---
layout: post
title:  "순열과 조합"
subtitle:   "DFS문제를 풀다가 순열과 조합이 헷갈려서 정리하는 포스팅. "
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 순열 
---

순서가 다르면 다르게 취급하는 것이 순열이다. [1, 3, 7]!=[1, 7, 3]

    '''c
	void DFS(int L){
		if(L==r){
			for(int j=0; j<L; j++){
				printf("%d ", res[j]);
			}
			cnt++;
			puts("");
		}
		else{
			for(int i=1; i<=n; i++){
				if(ch[i]==0){
					res[L]=a[i];
					ch[i]=1;
					DFS(L+1);
					ch[i]=0;
				}
			}
		}
	}

    '''

## 조합
---

부분집합과 같은 개념. [1, 3, 7]==[1, 7, 3] ~~부분집합은 조합으로 구하는 방법과 BFS으로 구하는 방법이 있다~~ 

    '''c
	void dfs(int s, int L){
		int i, j;
		if(L==r){
			for(j=0; j<L; j++){
				printf("%d ", ch[j]);
			}
			printf("\n");
		}
		else{
			for(i=s; i<n; i++){
					ch[L]=i;
					dfs(i+1, L+1);
			}
		}
	}

    '''


