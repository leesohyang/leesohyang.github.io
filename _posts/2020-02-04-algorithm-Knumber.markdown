---
layout: post
title:  "[프로그래머스] K번째 수"
subtitle:   "프로그래머스 K번째 수"
categories: algorithm
tags: algorithm 알고리즘 
comments: true
---


## 프로그래머스 K번째 수
---
 


    '''c

	#include <string>
	#include <vector>
	#include <algorithm>
	using namespace std;
	
	vector<int> solution(vector<int> array, vector<vector<int>> commands) {
	    vector<int> answer;
	    int i;
	    for(i=0;i<commands.size();i++){
	        vector<int> array2;
	        array2.assign(array.begin()+commands[i][0]-1, array.begin()+commands[i][1]); //end는 끝+1 까지. 
	        sort(array2.begin(), array2.end());
	        answer.push_back(array2[commands[i][2]-1]);
	        
	    }
	    return answer;
	}
    '''

