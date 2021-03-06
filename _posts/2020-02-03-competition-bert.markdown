---
layout: post
title:  "[2019 국어정보처리 경진대회]bert를 사용한 한국어 개체명 인식기"
subtitle:   "국어정보처리"
categories: competition
tags: competition
comments: true
header-img: img/post_img/bert.jpg
---

## 개요
> 2019년 국어 정보처리 경연대회에 참가하여 bert를 사용한 한국어 개체명 인식 시스템을 구현하고 공부한 내용을 정리한 포스팅입니다. 작성중에 있습니다. 

- 목차
	- [프로젝트의 시작](#프로젝트의-시작)
	- [BERT란 무엇인가?](#BERT란-무엇인가?) 
	- [Finetuning](#Finetuning)
	- [결과](#결과)

## 프로젝트의 시작  
---

이 프로젝트는 2019년 7월 멀티캠퍼스 자연어처리 과정 시작과 동시에 사람들과 팀을 꾸려서 수행하게 되었는데요, 비록 모델의 알려진 성능만큼 나오지 못하였고 수상도 하지 못하였지만 이때 여러 자료들을 찾아보고, 관련 컨퍼런스를 다니며 공부했던 것이 큰 도움이 되었습니다.  

## BERT란 무엇인가?
---
bert를 처음 접하는데 [논문](https://arxiv.org/abs/1706.03762)과 [게시글](http://docs.likejazz.com/bert/)에 큰 도움을 받았습니다. BERT란 2018년 11월 구글에서 공개한 최첨단 자연어처리 딥러닝 모델이며, 자연어처리 테스크를 비지도 학습으로 양방향 pretraining을 수행하는 첫 시스템입니다. 단어하나에 대한 왼쪽과 오른쪽 양쪽의 문맥을 deep 하게 표현하여 문장의 맥락을 학습시키게 됩니다.[Transformer]()

![screenshot](https://leesohyang.github.io/assets/img/post_img/bert2.jpg)
*BERT는 양방향, OpenAI GPT는 단방향, ELMO는 단방향이다.*

BERT는 결국 Tranformer를 기반으로 하여 사전 학습한 언어모델입니다. Tranformer가 뭔지 알기위해서는 우선 Attention mechanism에 대하여 알아야 하는데요, attention은 모든 sequence를 고려하면서 정보처리를 하지않고, 중요한 feature를 더욱 중요하게 고려하는 것을 모티브로 합니다. 작동원리는 다음과 같습니다. 
![screenshot2](https://leesohyang.github.io/assets/img/post_img/attention.PNG)
*Attention 모델 작동원리*
1. 기존 RNN모델에서 시작-파란색네모박스 
2. RNN셀의 각 output을 입력으로 하는 Feed forward fully connected layer
3. 2번 layer의 output을 각 RNN셀의 score로 결정합니다. 
4. 출력된 score에 softmax를 취한 값이 해당 셀의 Attention weight가 됩니다. 

Transformer는 이 attention mechanism에 RNN을 제거한 self-attention 을 사용한 모델입니다. 서로다른 인코더와 디코더가 6개씩 포진하고 있으며, 하나의 인코더 안에 self-attention과 feed forward 신경망이 들어있습니다. 트랜스포머의 학습 방법론은 여기서 다루지 않겠습니다. 

![screenshot4](https://leesohyang.github.io/assets/img/post_img/selfattention1.PNG)
*Self-Attention 모델 작동원리 1*

![screenshot3](https://leesohyang.github.io/assets/img/post_img/selfattention.PNG) 
*Self-Attention 모델 작동원리 2*


인코더에서는 각각이 512사이즈의 벡터로 단어를 임베딩(Token embedding)하여 신경망으로 전달합니다. BERT는 여기에 Position embedding 과 Segment embedding을 추가하여 총 3개의 임베딩을 합산한 결과를 취합니다. Position embedding은 각 토큰의 위치정보를 담으며, Segment embedding은 첫번째문장과 두번째 문장을 분류하는 역할을 합니다. 이를 코드로 나타내면 다음과 같습니다.

'''c

	embedding = self.token_embed(x)+self.position_embed(pos)+self.segment_embed(seg)

'''




## Finetuning
---
위와 같이 문맥적으로 표현된 단어토큰의 값들을 가지고 있는 pre-trained Bert모델을 NLP task에 사용하기 위해서는 모델 최상위층에 1개의 classification layer를 부착하면 됩니다. 
![screenshot4](https://leesohyang.github.io/assets/img/post_img/finetuning.png) 

BERT의 pretrained model은 ETRI에서 공개한 kobert모델을 사용하였습니다. 저희는 여기에 개체명 인식 테스크를 수행하도록 하기 위해 개체명 태깅된 데이터셋(ETRI 엑소브레인 말뭉치)에 대한 파인튜닝(fine-tuning)을 하였습니다. 아래 코드는 개체명(Ner) 태깅을 학습시킬 수 있는 파인튜닝 [소스](https://github.com/kyzhouhzau/BERT-NER)의 일부입니다. 

    
	```python
	
	class NerProcessor(DataProcessor):
	    def get_train_examples(self, data_dir):
	        return self._create_example(
	            self._read_data(os.path.join(data_dir, "train.txt")), "train"
	        )
	
	    def get_dev_examples(self, data_dir):
	        return self._create_example(
	            self._read_data(os.path.join(data_dir, "dev.txt")), "dev"
	        )
	
	    def get_test_examples(self,data_dir):
	        return self._create_example(
	            self._read_data(os.path.join(data_dir, "test.txt")), "test"
	        )
	
	
	    def get_labels(self):
	        """
	        here "X" used to represent "##eer","##soo" and so on!
	        "[PAD]" for padding
	        :return:
	        """
	        return ["[PAD]", "-", 
	                "PS_B", "PS_I", "LC_B", "LC_I", "OG_B", "OG_I", "DT_B", "DT_I", "TI_B", "TI_I", 
	                "X","[CLS]","[SEP]"]
	
	    def _create_example(self, lines, set_type):
	        examples = []
	        for (i, line) in enumerate(lines):
	            guid = "%s-%s" % (set_type, i)
	            texts = tokenization.convert_to_unicode(line[1])
	            labels = tokenization.convert_to_unicode(line[0])
	            examples.append(InputExample(guid=guid, text=texts, label=labels))
	        return examples
	
	'''

다음은 엑소브레인 말뭉치를 형태소 분석하여 개체명을 붙인 데이터의 예시입니다. 개체명 label은 BIO(B:begin, I:intermediate) 태깅을 사용하였습니다. 

![screenshot5](https://leesohyang.github.io/assets/img/post_img/ner.PNG)


