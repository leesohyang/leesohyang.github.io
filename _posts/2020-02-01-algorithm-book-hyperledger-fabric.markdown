---
layout: post
title:  "프로그래머스 DFS 타켓 넘버  문제 "
subtitle:   "프로그래머스 DFS 타켓 넘버  문제"
categories: algorithm
tags: algorithm 알고리즘 단어변환 DFS 프로그래머스 
comments: true
---


## 프로그래머스 단어변환 문제(DFS)



'''c

	#include <string>
	#include <vector>

	using namespace std;
	
	int total;
	
	void DFS(vector<int> &numbers, int &target, int L, int sum) {
	    if(L == numbers.size()){
	        if(sum == target) total++;
	    }else{
	
	    DFS(numbers, target, L+1, sum+numbers[L]);
	    DFS(numbers, target, L+1, sum-numbers[L]);
	    }
	}
	int solution(vector<int> numbers, int target) {
	    int answer = 0;
	
	    DFS(numbers, target, 0 , 0);
	    
	
	    answer = total;
	
	    return answer;
	}

'''




