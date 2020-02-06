---
layout: post
title:  "[삼성 SW 역량테스트] 휴가 문제"
subtitle:   "[삼성 SW 역량테스트] 휴가 문제"
categories: algorithm
tags: algorithm 알고리즘 
comments: true
---


## 문제 
---
![screenshot](https://leesohyang.github.io/assets/img/post_img/vacation.PNG)

## 코드
---
DFS(L+1, sum); <-- 여기에 else를 붙였다가 한참 해맸다 ㅠ.ㅠ
앞의 재귀가 끝난 후 무조건 돌아와서 수행되어야 하는 부분(L+1일 째부터 일 하는 경우)이므로 else를 붙이면 안됨... 


    '''c
	#include<stdio.h>
	#include<algorithm>
	#include<queue>
	#include<vector>
	using namespace std;
	int n, minx=-2147000000;
	vector<pair<int, int> > m[20];
	void DFS(int L, int sum){
		int i;
		if(L==n+1){
			if(sum>minx) minx=sum;
		}
		else {	
			if(L+m[L][0].first<=n+1) DFS(L+m[L][0].first, sum+m[L][0].second);
			DFS(L+1, sum); //else가 붙냐 안붙냐... 무조건 해야되니까.  
	}
		
		
	
	}
	int main(){
		freopen("input.txt", "rt", stdin);
		int i, a, b;
		scanf("%d", &n);
		for(i=1;i<=n;i++){
			scanf("%d %d", &a, &b);
			m[i].push_back(make_pair(a, b));
		}
		DFS(1, 0);
		printf("%d", minx);
		return 0;
	}
    '''

