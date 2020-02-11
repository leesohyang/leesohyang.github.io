---
layout: post
title:  "[프로그래머스] DFS 타켓 넘버  문제 "
subtitle:   "프로그래머스 DFS 타켓 넘버  문제"
categories: algorithm language
tags: algorithm language C++ 
comments: true
---


## 프로그래머스 타겟 넘버 문제(DFS)
---
dfs에서 부분집합을 구할때(쓰는경우DFS, 안쓰는경우 DFS)와 마찬가지로 +하는 재귀, -하는 재귀를 각각 써주면 된다.

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




