---
layout: post
title:  "[학위논문]C-LSTM을 사용한 한국어 감성분석"
subtitle:   "학위논문"
categories: projects
tags: projects thesis
comments: true
---

## 개요
> 학위논문으로 연구했던 프로젝트에 관한 포스팅입니다. .

- 목차
	- [서론](#서론) 
	- [연구 내용과 결론](#연구-내용과-결론)
	- [참고 문헌](#참고문헌)
  

## 서론 
---

4학년때 머신러닝 과목을 듣고 인공지능에 흥미가 생겨 관련 주제를 탐색하다가 자연어처리를 접하게 되었습니다. 이미지나 영상처리에 비해 아직 개발이 덜 되어있다고 생각했는데, 논문 연구를 마친 후 몇개월 사이에 Bert 모델이 나오면서 활발한 연구가 이루어지고 있네요. 
제가 연구한 내용은 자연어처리 분야에서 현재로써는 뒤처지는 모델이지만 첫 자연어처리 연구였음에 의의를 두고 포스팅을 시작하겠습니다. 

## 연구 내용과 결론  
---

[“A C-LSTM Neural Network for Text Classification.” , 2015 `](https://arxiv.org/abs/1511.08630)논문을 참고하여 CNN과 LSTM을 결합하여 한국어 영화리뷰 감성분석 모델을 연구, 구현하였습니다. 

CNN layer와 LSTM layer가 연결되는 모습은 다음과 같습니다. 위 논문에 따르면, LSTM의 입력의 sequence를 보장하기 위해 추출된 feature에 대한 maxpool은 수행하지 않습니다. 아래 그림의 빨간색 블록이 단어 "The"라고 가정하면, LSTM의 첫번째 입력은 CNN으로부터 추출된 "The"에 대한 feature값만을 합한 벡터가 됩니다.  
![screenshot](https://leesohyang.github.io/assets/img/post_img/thesis1.png)

모델 구현에 참고한 코드는 [다음](https://github.com/zackhy/TextClassification)과 같습니다. LSTM layer는 총 두개가 쌓여 사용되었습니다.

데이터는 [NSMC](https://github.com/e9t/nsmc) 데이터셋을 사용하였습니다. 각각의 영화 리뷰 별점이 9-10점이면 긍정으로, 1~4점이면 부정으로 labeling 하는 코드가 포함되어있습니다. 저는 여기에 중립의 label을 추가로 수집하여 총 세개의 label을 분류할 수 있도록 하였습니다.    

결과는 label이 긍정과 부정일때는 86%, 중립까지 포함하여 세개일때는 70%로, 이는 CNN단일모델과 비교하였을때 각각 약 1%, 2% 가량 높은 성능을 보였습니다. 모델이 복잡해진것에 비해서 딱히 눈에 띄지 않는 성과를 보여주었는데요, 이러한 결과를 분석해보기 위해 모델이 분류하지 못한 FN, FP 데이터를 직접 확인해보았습니다. 
(FN=False Negative, FP=False Positive)-confusion matrix

![screenshot2](https://leesohyang.github.io/assets/img/post_img/thesis2.PNG)

[Lime](https://dreamgonfly.github.io/2017/11/05/LIME.html)에서 영감을 받아 모델의 분류 근거를 시각화하는 코드를 작성하였습니다. TP, TN, FP, FN 네가지 경우에 대한 시각화 한 결과는 다음과 같습니다. 
![screenshot3](https://leesohyang.github.io/assets/img/post_img/4.png)


위와 같이 모델이 분류하지 못한 문장에 대해서 분류 근거를 예측하여 보았는데, 첫 번째로 형태소 분석이 올바르게 되지 않은 경우가 많았습니다. 이는 원래 문장 데이터가 맞춤법이 틀린 경우가 많고 띄어쓰기가 되어있지 않은 문장이 다수 있었기 때문인데, 모델에 입력하기전 전처리가 필요하다는 것을 느낄 수 있었습니다. 두 번째로 자연어의 특성상 독창적인 표현 패턴이 다양하게 존재하다 보니, 각 상황에 맞게 단어의 의미대로 올바르게 가중치가 학습되어야 하는데 이것이 부족하였던 것으로 보입니다. 이를 보완하기 위한 방법으로는 사전에 광대한 양의 데이터로부터 학습된 단어벡터를 삽입하거나, 모델이 희소성 있는 표현이더라도 충분히 학습할 수 있도록 훈련 데이터의 양을 늘리는 방법이 있을 것입니다.  
향후에 모델이 분류에 실패하는 오류 패턴에 대해서 추가적으로 분석하고, 그에 맞게 데이터를 늘리거나, 사전 학습된 단어벡터를 삽입하여 모델을 학습시킨다면 보다 높은 성능으로 감성 분류를 수행 할 수 있을 것으로 예상됩니다. 

## 참고 문헌 
---