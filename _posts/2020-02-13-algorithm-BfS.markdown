---
layout: post
title:  "BFS 미로 최단거리 구하기"
subtitle:   "BFS 미로 최단거리 구하기"
categories: algorithm language 
tags: algorithm language C++
comments: true
---


## BFS
---
무언가의 최단거리를 구할 땐 BFS, 최소비용을 구할땐 DFS를 사용한다. BFS는 따로 2차원 배열을 만들어놓고 인접한 지점으로 이동할때마다 +1 해준다. 한칸씩 이동하면서(같은곳 또 안가도록 checking 해주면서) 그 지점까지 걸린 거리를 업데이트 하는 것(queue를 통해서 상하 좌우 무조건 한칸씩 이동하므로 +1씩 해주면 된다.)과 같다. 

    '''c
	#include<bits/stdc++.h>
	#define x first
	#define y second
	using namespace std;
	int dx[4]={-1, 0, 1, 0};
	int dy[4]={0, 1, 0, -1};
	int main(){
		ios_base::sync_with_stdio(false);
		freopen("input.txt", "rt", stdin);
		vector<vector<int> > board(7, vector<int>(7, 0));
		vector<vector<int> > dis(7, vector<int>(7, 0));
		queue<pair<int, int> > Q;
		for(int i=0; i<7; i++) {
			for(int j=0; j<7; j++) {
				cin>>board[i][j];
			}
		}
		Q.push(make_pair(0, 0));
		board[0][0]=1;
		while(!Q.empty()) {
			pair<int, int> tmp = Q.front();
			Q.pop();
			for(int i=0; i<4; i++) {
				int x=tmp.x+dx[i];
				int y=tmp.y+dy[i];
				if(x>=0 && x<7 && y>=0 && y<7 && board[x][y]==0) {
					Q.push(make_pair(x, y));
					board[x][y]=1;
					dis[x][y] = dis[tmp.x][tmp.y] + 1;
				}
			}
		}
		if(dis[6][6]==0) cout<<"-1";	
		else cout<<dis[6][6];
		return 0;
	}
    '''

