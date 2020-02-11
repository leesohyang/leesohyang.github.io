---
layout: post
title:  "[프로그래머스] H-Index"
subtitle:   "프로그래머스 H-Index"
categories: algorithm language
tags: algorithm language C++ 
comments: true
---


## 프로그래머스 H-Index
---
H-Index는 말 그대로 index값을 물어보는 것이다. 
테스트케이스 9번은 [100, 50, 10]-3
인덱스가 배열값보다 커지는 경우가 없으면 전체 배열 크기를 리턴하면 된다. 


    '''c

	#include <string>
	#include <vector>
	#include <algorithm>
	using namespace std;
	bool bigger(int a, int b){
	    return a>b;
	}
	int solution(vector<int> citations) {
	    int answer = 0;
	    int i;
	    bool flag=false;
	    sort(citations.begin(), citations.end(), bigger);
	    for(i=0;i<citations.size();i++){
	        if(i>=citations[i]){
	            answer=i;
	            flag=true;
	            break;
	        }else continue;
	    }
	    if(!flag) answer=citations.size();
	    
	    return answer;
	}
    '''

