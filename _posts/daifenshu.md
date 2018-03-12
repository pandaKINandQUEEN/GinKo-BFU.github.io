---
layout:     post
title:      "带分数"
subtitle:   ""
date:       2018-03-12
author:     "JinTao"
header-img: "img/lanqiao.jpg"
catalog: true
tags:
- 蓝桥杯
---

## 带分数

### 描述
100 可以表示为带分数的形式：100 = 3 + 69258 / 714。
还可以表示为：100 = 82 + 3546 / 197。
注意特征：带分数中，数字1~9分别出现且只出现一次（不包含0）。
类似这样的带分数，100 有 11 种表示法。
### 输入
从标准输入读入一个正整数N (N<1000*1000)
### 输出
程序输出该数字用数码1~9不重复不遗漏地组成带分数表示的全部种数。
注意：不要求输出每个表示，只统计有多少表示法！
### 样例输入1 
100

### 样例输出1 
11

### 样例输入2
105

### 样例输出2
6


### Exp
本以为这是一道水题，但由于经验不足A了三个小时。<br>
1.用 substr()+stringstream转数字 等不出结果，我早该聊到sstream的速度了。<br>
2.用 substr()+stoll()转数字，dev竟然还不支持c++11,好吧，工具->编译选项->编译时加入以下命令->-std=c++11搞定；<br>
3.我日？蓝桥网不知持C++11?!<br>
4.好吧，不支持算了，然后企图在本地找到stoll()函数原型，无果；<br>
5.你大爷找不到我自己写个stoll。<br>
6.超时；<br>
7.一定是substr()浪费了时间，用vector<int>吧(以前写next_permutation()没有和数组配合过，所以首选了vector)<br>
8.超时<br>
9.优化，比以前快两倍左右<br>
10.超时<br>
11.各种微乎其微的优化<br>
12.TLE<br>
13.本人已疯<br>
14.难道是next_permutation()效率太低？？<br>
....<br>
n.是不是c++效率太低啊，vector换成数组试试吧<br>
n+1.Accept!<br>
一番测试，同一组数据，普通数组的效率约为vector的15倍。<br>
一下午A一道大水题也真是令人绝望..<br>

### AC代码
``` cpp
#include<iostream>

#include<cstring>

#include<sstream>

#include<algorithm>

#include<cstdlib>

#include<ctime>

#include<vector>

using namespace std;
int s[9];
int stoll(int I,int J)
{
	int ans=0;
	

	for(int i=I;i<=J;i++)
	{
		ans=ans*10+s[i];
	}
	return ans;
}

int main()
{
	int n;
	scanf("%d",&n);
	
	
	for(int i=0;i<9;++i)	s[i]=i+1;
	
	int cnt=0;
	
	double st=clock();
	
	do{
		for(int i=1;i<=7;++i)
		{
			int z=stoll(0,i-1); 
			if(z<n)
				for(int j=i+(10-i)/2;j<9;++j)
				{
					int t,b;
					
					t=stoll(i,j-1);
					
					b=stoll(j,8);
					
					if(t%b==0&&(z+t/b)==n)	cnt++;
				}
		}
		
	}while(next_permutation(s,s+9));
	
	printf("%d\n",cnt);
	
	double et=clock();
	
	printf("%lfms\n",et-st);
	return 0;
} 
```

