---
layout:     post
title:      "ZYQ与大哥"
subtitle:   ""
date:       2018-01-22
author:     "JinTao"
header-img: "img/head2.jpg"
catalog: true
tags:
- ACM
---

## ZYQ与大哥

这题乍看上去很简单，但很遗憾暴力会T.愿意就是ZYQtmd有太多狗子了n^2一定超时

一开始题意理解的也不好，注意a能被b整除意味着a%b=0(a是被除数)，a除以b=a除用b=a/b

### 描述
ZYQ让N(1≤N≤100000)只狗子坐成一个圈．除了1号与N号狗子外，i号狗子与i-l号和i+l号狗子相邻．N号狗子与1号狗子相邻．ZYQ用很多纸条装满了一个桶，每一张包含了一个1到1,000,000的数字．

接着ZYQ让每一只狗子 i 从柄中取出一张纸条Ai作为他的编号。

每只狗轮流走上一圈，同时摸所有其他编号能被他的编号整除的狗的狗头，然后坐回到原来的位置。

狗子们希望你帮助他们确定，每一只狗子需要摸的狗头。
### 输入
第1行包含一个整数N，接下来第2到N+1行每行包含一个整数Ai．
### 输出
第1到N行，每行的输出表示第i头狗子要的狗头的数量．
### 样例输入1 
5<br>
2<br>
1<br>
2<br>
3<br>
4

### 样例输出1 
2<br>
0<br>
2<br>
1<br>
3

### AC
``` cpp
#include<iostream>

#include<cstring>

#include<string>

using namespace std;
int a[1000003];//标记编号出现的次数

int b[1000003];
int x[1000003];//因为每只狗拿到的编号可能会重复，用x记录下第i只狗拿到的是x[i]号

int main()
{
	int n;
	while(cin>>n)
	{
		int max=-1;
		memset(a,0,sizeof(a));
		memset(b,0,sizeof(b));
		for(int i=0;i<n;++i)
		{
			int t;
			scanf("%d",&t);
			a[t]+=1;//记录次数
			
			x[i]=t;
			if(t>max)
			 max=t;
		}
		for(int i=1;i<=max;++i)
		{
			if(a[i])
			{
				for(int j=i;j<=max;j+=i)
				{
					b[j]+=a[i];
				}
			}
		}
		for(int i=0;i<n;++i)
		{
			cout<<b[x[i]]-1<<endl;
		}
	}
	return 0;
}
```

