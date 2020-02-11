---
layout: post
title:  "위상정렬"
subtitle:   "위상정렬"
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 위상정렬
---

인접행렬(유방향)+ 진입차수(몇개로부터 들어오는지) 따로 저장 필요-0이여야 바로 수행될수 있으므로 큐 삽입, 큐 삽입 후 pop하고 연결노드 찾고 진입차수 감소시켜줌. 


    '''c

	#include<stdio.h>
	#include<vector>
	#include<queue>
	#include<algorithm>
	using namespace std;
	int main(){
		freopen("input.txt", "rt", stdin);	
		int n, m, a, b, score;
		scanf("%d %d", &n, &m);
		vector<vector<int> > graph(n+1, vector<int>(n+1, 0));
		vector<int> degree(n+1);
		queue<int> Q;
		for(int i=0; i<m; i++){
			scanf("%d %d", &a, &b);
			graph[a][b]=1;
			degree[b]++;
		}
		for(int i=1; i<=n; i++){
			if(degree[i]==0) Q.push(i);
		}
		while(!Q.empty()){
			int now=Q.front();
			Q.pop();
			printf("%d ", now);
			for(int i=1; i<=n; i++){
				if(graph[now][i]==1){
					degree[i]--;
					if(degree[i]==0) Q.push(i);
				}
			}
		}
		return 0;
	}
	

    '''

