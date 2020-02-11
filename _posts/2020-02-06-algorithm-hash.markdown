---
layout: post
title:  "[프로그래머스] 위장 문제"
subtitle:   "프로그래머스 위장 문제"
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 프로그래머스 위장 문제 
---

hash를 사용하는 문제이다. c는 학교다닐때 배운게 다인데 알고리즘 공부를 c++로 하고있다. 그래서 오늘 hash iterator를 처음 공부했다... 구글링하면서... 다음 [링크](https://kamang-it.tistory.com/entry/mapunorderedmapC%EC%97%90%EC%84%9C-map%EB%94%95%EC%85%94%EB%84%88%EB%A6%ACdictionary-%EC%97%B0%EA%B4%80%EB%B0%B0%EC%97%B4associate-array%ED%95%B4%EC%8B%9C%EB%A7%B5hash-map%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0map%EA%B3%BC-unorderedmap-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%B0%A8%EC%9D%B4%EC%A0%90)를 참조하였는데 많은 도움이 되었다.
여기서 사용한 해쉬구조인 unordered_map말고 다른 자료구조들도 많은 것 같던데 잘 모르겠다.    

hash는 둘째치고 이 문제 풀이에서 가장 놀라웠던 점은 모든 조합의 갯수를 구하는 방법이 아주 간단하였다. 

-상의 3종류
-하의 2종류
-안경 4종류

라고 쳤을때 이 문제에서 요구하는 서로 다른 옷들의 조합의 수(안경하나만 입어도된다.)는 

-상의 3(종류)+1(선택 안 한 경우)
-하의 2(종류)+1(선택 안 한 경우)
-안경 4(종류)+1(선택 안 한 경우)

를 모두 곱한 것, 즉 4*3*5 에 모두 안 입을수는 없으니 1을 빼주면 된다. ~~충격적~~ 

    '''c

	#include <string>
	#include <vector>
	#include <unordered_map>
	#include <iostream>
	
	using namespace std;
	
	int solution(vector<vector<string>> clothes) {
	    unordered_map<string, int> map;
	    vector<string> name;
	    int answer = 1, tmp=1;
	    int i;
	    int x=clothes.size();
	    for(i=0;i<clothes.size();i++){
	        map[clothes[i][1]]++;
	       
	    }
	    unordered_map<string, int>::iterator it; 
	    for (pair<string, int> atom : map) {
	        answer*=atom.second+1;
	    }
	    answer-=1;
	    return answer;
	}
    '''

