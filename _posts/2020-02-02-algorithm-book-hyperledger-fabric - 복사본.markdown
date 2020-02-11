---
layout: post
title:  "[프로그래머스] DFS 단어변환 문제 "
subtitle:   "프로그래머스 DFS 단어변환 문제"
categories: algorithm language
tags: algorithm language C++ 
comments: true
---


## 프로그래머스 단어변환 문제(DFS)



'''c

	#include <string>
	#include <vector>
	int cnt=0, minx=2147000000;
	using namespace std;
	bool flag=false;
	vector<int> ch(60);
	void DFS(string begin, string &target, int sum, vector<string> &words){
	    int i, j, k;
	    string word;
	    // bool flag=false;
	    
	    if(begin==target){
	        if(sum<minx){
	            minx=sum;
	            flag=true;
	        }
	    }else{
	        for(i=0;i<words.size();i++){
	            word=words.at(i);
	            
	            int same=0;
	            for(j=0;j<begin.size();j++){
	      
	                if(begin.at(j)==word.at(j)) same++;
	                
	            }if(same==begin.size()-1){
	                if(ch[i]==0){
	                    ch[i]=1;
	                    DFS(word, target, sum+1, words);
	                    ch[i]=0;
	                } 
	            }
	        }
	    }
	}
	int solution(string begin, string target, vector<string> words) {
	    int answer = 0;
	    DFS(begin, target, 0, words);
	    if(flag) answer=minx;
	
	    return answer;
	}

'''

아래는 테스트 화면입니다. 

![screenshot](https://leesohyang.github.io/assets/img/projects/KakaoTalk_20200202_171035151.png)


