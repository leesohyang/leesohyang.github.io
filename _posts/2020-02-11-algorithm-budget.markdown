---
layout: post
title:  "[프로그래머스] 예산 문제"
subtitle:   "예산 문제"
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 예산 문제 - 이분탐색 
---

간단한 이분탐색 문제이다. while문 안에 lt와 rt의 조건에 같거나 작다에서 같다를 빼먹었다가 한참 고생하였다. 이분탐색 조건에서 lt<=rt 항상 주의하자. 


    '''c

	#include <string>
	#include <vector>
	
	using namespace std;
	
	int solution(vector<int> budgets, int M) {
	    int answer = 0, rt=0, lt=1, mid=0, tmp=0, maxin=-2147000000;
	    
	    for(int i=0;i<budgets.size();i++){
	        if(budgets[i]>rt) rt=budgets[i];
	    }
	    while(lt<=rt){
	        int sum=0;
	        mid=(lt+rt)/2; //상한가
	        for(int i=0;i<budgets.size();i++){
	            if(budgets[i]<=mid) sum+=budgets[i];
	            else sum+=mid;
	        }
	        if(sum<=M) {
	            lt=mid+1; //상한가를 좀더 높여보자
	            if(sum>maxin){
	                maxin=sum;
	                answer=mid;
	            }
	        }
	        else if(sum>M){ //상한가를 내려
	            rt=mid-1;
	        }
	    }
	
	    return answer;
	}

    '''

