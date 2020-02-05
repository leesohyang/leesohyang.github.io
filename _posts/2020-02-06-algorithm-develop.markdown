---
layout: post
title:  "[프로그래머스] 기능개발"
subtitle:   "프로그래머스 기능개발"
categories: algorithm
tags: algorithm 알고리즘 
comments: true
---


## 프로그래머스 기능개발 
---

굳이 queue를 쓸 필요는 없었던 것 같다. 


    '''c

	#include <string>
	#include <vector>
	#include <queue>
	
	using namespace std;
	
	vector<int> solution(vector<int> progresses, vector<int> speeds) {
	    vector<int> answer;
	    int x;
	    queue<int> Q;
	    int i, j, cnt=1;
	    for(i=0;i<progresses.size();i++){
	        if((100-progresses[i])%speeds[i]!=0){
	             Q.push((100-progresses[i])/speeds[i]+1);
	        }else Q.push((100-progresses[i])/speeds[i]);
	    }
	    while(!Q.empty()){
	        x=Q.front();
	        Q.pop();
	        while(1){
	            if(Q.empty()){
	                answer.push_back(cnt);
	                break;
	            }
	            if(Q.front()<=x){
	                Q.pop();
	                cnt++;
	            }else{
	                answer.push_back(cnt);
	                cnt=1;
	                break;
	            }
	        }
	    }
	    return answer;
	}
    '''

