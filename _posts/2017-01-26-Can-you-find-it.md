---
layout:     post
title:      "Can you find it?"
subtitle:   ""
date:       2017-01-26
author:     "JinTao"
header-img: "img/head2.jpeg"
catalog: true
tags:
- ACM
- 二分
---

## Can you find it? 
这道题真的是A了一下午，各种错误情况都遇见了。总结一下：

分析复杂度！！！！！当然我一开始就知道暴力搜索一定超时，要用二分查找，但还是T;

因为没抓住重点，这道题利用二分查找（nlogn）将复杂度，那应该在生成的那个最长的数组里做二分查找

用最长500的数组做外层循环，这样的优化才彻底。


### 描述
Give you three sequences of numbers A, B, C, then we give you a number X. Now you need to calculate if you can find the three numbers Ai, Bj, Ck, which satisfy the formula Ai+Bj+Ck = X.

### 输入
There are many cases. Every data case is described as followed: In the first line there are three integers L, N, M, in the second line there are L integers represent the sequence A, in the third line there are N integers represent the sequences B, in the forth line there are M integers represent the sequence C. In the fifth line there is an integer S represents there are S integers X to be calculated. 1<=L, N, M<=500, 1<=S<=1000. all the integers are 32-integers.

### 输出
For each case, firstly you have to print the case number as the form "Case d:", then for the S queries, you calculate if the formula can be satisfied or not. If satisfied, you print "YES", otherwise print "NO".
### 样例输入1 
3 3 3<br>
1 2 3<br>
1 2 3<br>
1 2 3<br>
3<br>
1<br>
4<br>
10<br>

### 样例输出1 
Case 1:<br>
NO<br>
YES<br>
NO<br>

#### AC代码
``` cpp
#include<iostream>

#include<algorithm>

using namespace std;
int a[550],b[550],c[550];
int d[250050];
int search(int n,int s,int e)
{
	if(s<=e)
	{
		int m=(s+e)/2;
		if(n==d[m])	return 1;
		else if(d[m]>n)	search(n,s,m-1);
		else search(n,m+1,e);
	}
	else
		return 0;
}
int main()
{
	int n1,n2,n3;int cas=0;
	while(cin>>n1>>n2>>n3)
	{
		cas++;
		for(int i=0;i<n1;++i)	cin>>a[i];
		for(int i=0;i<n2;++i)	cin>>b[i];
		for(int i=0;i<n3;++i)	cin>>c[i];
		int cnt=0;
		for(int i=0;i<n1;++i)
			for(int j=0;j<n2;++j)
			{
				d[cnt++]=a[i]+b[j];
			}
		sort(d,d+cnt);
		int n;cin>>n;
		cout<<"Case "<<cas<<":"<<endl;
		while(n--)
		{
			int flag=0;int t;cin>>t;
			for(int i=0;i<n3;++i)
			{
				if(search(t-c[i],0,cnt-1))
				{
					flag=1;
					break;
				}
			}
			if(flag)	cout<<"YES"<<endl;
			else	cout<<"NO"<<endl;
		}
	}
	return 0;
}
```

#### WA
一直WA的代码也附上，真不知道一样的代码，重写一遍就过了，希望有一天能找到原因 So,can you find it?
```cpp
#include<iostream>

#include<cstdio>

#include<cstring>

#include<algorithm>

#include<cstring>

using namespace std;
int a[1000],b[1000],c[1000];
int se[1000000];
int search(int n,int s,int e)
{
	if(s<=e)
	{
		int m=(s+e)/2;
		if(n==se[m]) return 1;
		else if(se[m]<n)  search(n,m+1,e);
		else search(n,s,m-1);
	}
	else
	return 0;
}
int main()
{
	int n1,n2,n3;int I=0;
	while(scanf("%d%d%d",&n1,&n2,&n3)!=EOF)
	{
		
		I++;int ii=0;
		for(int i=0;i<n1;++i) scanf("%d",&a[i]);
		for(int i=0;i<n2;++i) scanf("%d",&b[i]);
		for(int i=0;i<n3;++i) scanf("%d",&c[i]);
		
		for(int i=0;i<n1;++i)
				for(int j=0;j<n2;++j)
				{
					se[ii++]=a[i]+b[j];
				}
		sort(c,c+n3);
		sort(se,se+ii);
		int n;scanf("%d",&n);
		cout<<"Case "<<I<<"."<<endl;
		for(int X=0;X<n;++X)
		{
			int flag=0;int d;cin>>d;
			for(int i=0;i<n3;++i)
			{
				if(search(d-c[i],0,ii-1))
				{
					flag=1;
				}
			}
			if(flag) cout<<"YES"<<endl;
			else cout<<"NO"<<endl;
		}
	}
	return 0;
}
```

