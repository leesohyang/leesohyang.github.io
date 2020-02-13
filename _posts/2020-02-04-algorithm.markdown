---
layout: post
title:  "[프로그래머스] DFS 여행경로 문제"
subtitle:   "프로그래머스 DFS 여행경로 문제"
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 프로그래머스 여행경로 문제(DFS)
---
문제 조건 1 ) 주어진 항공권은 모두 사용해야 합니다.

문제 조건 2 ) 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.

조건2를 좀더 쉽게 풀기 위해 애초에 주어지는 티켓 리스트를 알파벳순서로(오름차순) sort 시켰다. 문제는 이렇게 해놓을 경우 DFS에서 사용한 티켓 개수가 tickets.size()일때 무조건 처음 걸린(처음으로 티켓 전부 완주한 케이스)만이 정답이다. 오름차순 sorting 되어있기 땜에... 

따라서 if(max_cnt < cnt)인 경우에만 정답벡터에 삽입한다. 그 다음 완주한 cnt는 그 전 max_cnt보다 크지 못하므로, 그냥 무시된다.


    '''c

	#include <string>
	#include <vector>
	#include <algorithm>
	
	using namespace std;
	
	int max_cnt = 0;
	
	void DFS(string start, vector<vector<string>>& tickets, vector<bool>& visit, vector<string>& answer, vector<string>& temp, int cnt) {
	    temp.push_back(start);
	    
	    if (max_cnt < cnt) {
	        max_cnt = cnt;
	        answer = temp;
	    }
	    
	    for (int i = 0; i < tickets.size(); i++) {
	        if (start == tickets[i][0] && !visit[i]) {
	            visit[i] = true;
	            DFS(tickets[i][1], tickets, visit, answer, temp, cnt + 1);
	            visit[i] = false;
	            temp.pop_back();
	        }
	    }
	    
	}
	
	vector<string> solution(vector<vector<string>> tickets) {
	    int cnt = 0;
	    vector<string> answer, temp;
	    vector<bool> visit(tickets.size(), false);
	    sort(tickets.begin(), tickets.end());
	    DFS("ICN", tickets, visit, answer, temp, cnt);
	    return answer;
	}
    '''

