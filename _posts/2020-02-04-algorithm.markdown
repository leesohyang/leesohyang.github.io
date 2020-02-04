---
layout: post
title:  "[프로그래머스] DFS 여행경로 문제"
subtitle:   "프로그래머스 DFS 여행경로 문제"
categories: algorithm
tags: algorithm 알고리즘 
comments: true
---


## 프로그래머스 여행경로 문제(DFS)
---
주어진 항공권을 모두 사용해야만 하는 문제입니다. "가능한 경로" 중 알파벳 우선순위로 찾으라 해서 헷갈렸는데 항공권을 모두 사용하지 않는 경로는 불가능한 경로더군요...!!
따라서 불가능하면 다음 우선순위인 알파벳 항공권을 사용해야하는 문제입니다. 
DFS에서 다음 항공권을 찾지 못하면 체크를 풀면서 돌아오되 지금까지 사용한 맥시멈 티켓수를 저장해놔야 합니다. max_cnt 와 cnt가 그것입니다. 


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

