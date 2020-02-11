---
layout: post
title:  "[프로그래머스] 가장 큰 수"
subtitle:   "프로그래머스 가장 큰 수"
categories: algorithm language
tags: algorithm language C++
comments: true
---


## 프로그래머스 가장 큰 수
---
 
정렬함수 sort() custom하기 

    '''c

	#include <string>
	#include <vector>
	#include <algorithm>
	using namespace std;
	bool bigger(string a, string b){
	    return a+b>b+a;
	}
	string solution(vector<int> numbers) {
	    string answer = "";
	    vector<string> tmp;
	    int i;
	    for(i=0;i<numbers.size();i++){
	        tmp.push_back(to_string(numbers[i]));
	    }
	    sort(tmp.begin(), tmp.end(), bigger);
	    for(i=0;i<numbers.size();i++){
	        answer+=tmp.at(i);
	    }
	    
	    if (tmp.at(0) == "0") return "0"; //와 예외처리;
	    return answer;
	}
    '''

