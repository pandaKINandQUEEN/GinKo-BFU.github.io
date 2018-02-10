---
layout:     post
title:      "A Knight's Journey"
subtitle:   ""
date:       2018-02-09
author:     "JinTao"
header-img: "img/head2.jpg"
catalog: true
tags:
- ACM
- dfs
---

## A Knight's Journey

### 描述
Background 
The knight is getting bored of seeing the same black and white squares again and again and has decided to make a journey 
around the world. Whenever a knight moves, it is two squares in one direction and one square perpendicular to this. The world of a knight is the chessboard he is living on. Our knight lives on a chessboard that has a smaller area than a regular 8 * 8 board, but it is still rectangular. Can you help this adventurous knight to make travel plans? 

Problem 
Find a path such that the knight visits every square once. The knight can start and end on any square of the board.
### 输入
The input begins with a positive integer n in the first line. The following lines contain n test cases. Each test case consists of
a single line with two positive integers p and q, such that 1 <= p * q <= 26. This represents a p * q chessboard, where p describes 
how many different square numbers 1, . . . , p exist, q describes how many different square letters exist. These are the first q 
letters of the Latin alphabet: A, . . .
### 输出
The output for every scenario begins with a line containing "Scenario #i:", where i is the number of the scenario starting at 1. Then print a single line containing the lexicographically first path that visits all squares of the chessboard with knight moves followed by an empty line. The path should be given on a single line by concatenating the names of the visited squares. Each square name consists of a capital letter followed by a number. 
If no such path exist, you should output impossible on a single line.
### 样例输入1 
3<br>
1 1<br>
2 3<br>
4 3

### 样例输出1 
Scenario #1:<br>
A1<br><br>

Scenario #2:<br>
impossible<br><br>

Scenario #3:<br>
A1B3C1A2B4C2A3B1C3A4B2C4<br><br>

### AC
#include<iostream>

#include<cstring>

using namespace std;
int x[8]={-1,1,-2,2,-2,2,-1,1};

int y[8]={-2,-2,-1,-1,1,1,2,2};
int sign[10][10];
int flag;
int m,n;
void search(int u,int v,int I);
int main()
{
	int T;cin>>T;
	for(int I=1;I<=T;++I)
	{
		flag=0;
		memset(sign,0,sizeof(sign));
		cin>>m>>n;
		cout<<"Scenario #"<<I<<":"<<endl;
		sign[1][1]=1;
		search(1,1,1);
		
		if(flag==0)	cout<<"impossible"<<endl<<endl;
		
	}
	return 0;
}
void search(int u,int v,int I)
{
	if(I==m*n)
	{
		flag=1;
		int cnt=1;
		while(cnt<=m*n)
		{
			for(int i=1;i<=m;++i)
			{
				for(int j=1;j<=n;++j)
				{
					if(sign[i][j]==cnt)
						cout<<(char)(j+64)<<i;
				}
			}
			cnt++;
		}
		cout<<endl;
		cout<<endl;
	}

	if(flag==0)
		for(int i=0;i<8;++i)
		{
			if((u+x[i]>=1)&&(u+x[i]<=m)&&
				(v+y[i]>=1)&&(v+y[i]<=n)&&
					sign[u+x[i]][v+y[i]]==0)	
			{
				sign[u+x[i]][v+y[i]]=I+1;
				search(u+x[i],v+y[i],I+1);
				sign[u+x[i]][v+y[i]]=0;
			}
		}	
} 

```

