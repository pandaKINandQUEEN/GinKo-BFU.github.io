---
layout:     post
title:      "Train Problem I"
subtitle:   ""
date:       2017-01-23
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    - stack
    - ACM
    - queue
    
---

## Train Problem I
这题第一次WA了，因为“Yes.”没加“.”
判断栈操作是否合法有技巧例如12345->24315就是合法的，
而12345->24135就不合法因为在4之后比4小的1和3不是降序的

### 描述
As the new term comes, the Ignatius Train Station is very busy nowadays. A lot of student want to get back to school by train(because the trains in the Ignatius Train Station is the fastest all over the world ^v^). But here comes a problem, there is only one railway where all the trains stop. So all the trains come in from one side and get out from the other side. For this problem, if train A gets into the railway first, and then train B gets into the railway before train A leaves, train A can't leave until train B leaves. The pictures below figure out the problem. Now the problem for you is, there are at most 9 trains in the station, all the trains has an ID(numbered from 1 to n), the trains get into the railway in an order O1, your task is to determine whether the trains can get out in an order O2.

### 输入
The input contains several test cases. Each test case consists of an integer, the number of trains, and two strings, the order of the trains come in:O1, and the order of the trains leave:O2. The input is terminated by the end of file. More details in the Sample Input.

### 输出
The output contains a string "No." if you can't exchange O2 to O1, or you should output a line contains "Yes.", and then output your way in exchanging the order(you should output "in" for a train getting into the railway, and "out" for a train getting out of the railway). Print a line contains "FINISH" after each test case. More details in the Sample Output. 

### 样例输入1 
3 123 321<br>
3 123 312

### 样例输出1 
Yes.<br>
in<br>
in<br>
in<br>
out<br>
out<br>
out<br>
FINISH<br>
No.<br>
FINISH<br>


``` cpp
#include<iostream>

#include<stack>

#include<queue> 

#include<cstring>

using namespace std;
int main()
{
	int n;string s1,s2;
	while(cin>>n>>s1>>s2)
	{
		int a[10000];int f=1;
		memset(a,0,sizeof(a));
		stack<char>s; queue<char>q1,q2;
		for(int i=0;i<n;++i)
		{
			q1.push(s1[i]);
			q2.push(s2[i]);
		}
		while(1)
		{
			while((!s.empty())&&(s.top()==q2.front()))
			{
				s.pop();q2.pop();
				a[f++]=0;
			}
			if(!q1.empty())
			{
				s.push(q1.front());
				a[f++]=1;
				q1.pop();
			}
			else
			{
				break;
			}
		}
		if(q2.empty())
		{
			cout<<"Yes."<<endl;
			for(int i=1;i<f;++i)
			{
				if(a[i])	cout<<"in"<<endl;
				else	cout<<"out"<<endl; 
			}
		}
		else
		{
			cout<<"No."<<endl;
		}
		cout<<"FINISH"<<endl;
	}
}
```

