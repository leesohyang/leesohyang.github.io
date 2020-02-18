---
layout: post
title:  "순열과 조합"
subtitle:   "DFS문제를 풀다가 순열과 조합이 헷갈려서 정리하는 포스팅. "
categories: algorithm language
tags: algorithm language C++
comments: true
---

## 개요
---
DFS를 사용한 순열과 조합, 조합(부분집합)중에서도 여러 방법이 있는데 이를 정리하기 위한 포스팅입니다. **재귀는 꼭 트리를 그려서 동작을 확인할 것.** 

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

부분집합과 같은 개념. [1, 3, 7]==[1, 7, 3] ~~부분집합은 조합으로 구하는 방법과 BFS으로 구하는 방법이 있다~~ 가장 큰 차이점은 for문의 유무 이다.

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

BFS(넓이우선탐색)와 같은 방식으로 부분집합을 구하는 방법은 아래와 같다. 두개의 갈래로 나뉘는데 이는 해당 원소를 사용한다 vs 안한다 를 의미한다. 

	'''c
	void DFS(int L, int cnt){
		if(L>pz.size()) return;
		if(cnt==m){
			sum=0;
			for(int i=0; i<hs.size(); i++){
				int x1=hs[i].first;
				int y1=hs[i].second;
				dis=2147000000;
				for(int j=0; j<m; j++){
					int x2=pz[ch[j]].first;
					int y2=pz[ch[j]].second;
					dis=min(dis, abs(x1-x2)+abs(y1-y2));
				}
				sum=sum+dis;
			}
			if(sum<res) res=sum;
		}
		else{
			ch[cnt]=L;
			DFS(L+1, cnt+1);
			DFS(L+1, cnt);
		}
	}
	'''

