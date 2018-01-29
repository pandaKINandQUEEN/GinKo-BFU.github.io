---
layout:     post
title:      "Inversion"
subtitle:   ""
date:       2018-01-29
author:     "JinTao"
header-img: "img/head2.jpg"
catalog: true
tags:
- ACM
- 二分
---

## Inversion 
仔细想想这道题无论怎么做都会有一条必经之路，那就是求一个序列的逆序对个数。

“adjacent” 题目中说每次交换相邻的两个数，这样每次交换都会使逆序对数减一(当还有逆序对存在)。

只要这个序列不是上升序列就一定有逆序对存在。

最后：除了int main(),把所有的int替换为 long long 才过

### 描述
bobo has a sequence a 1,a 2,…,a n. He is allowed to swap two adjacent numbers for no more than k times. 

Find the minimum number of inversions after his swaps. 

Note: The number of inversions is the number of pair (i,j) where 1≤i<j≤n and a i>a j.
### 输入
The input consists of several tests. For each tests: 

The first line contains 2 integers n,k (1≤n≤10 5,0≤k≤10 9). The second line contains n integers a 1,a 2,…,a n (0≤a i≤10 9).
### 输出
For each tests: 

A single integer denotes the minimum number of inversions.
### 样例输入1 
3 1<br>
2 2 1<br>
3 0<br>
2 2 1

### 样例输出1 
1<br>
2

### AC
``` cpp
#include<iostream>

using namespace std;
long long a[100050];
long long t[100050];
long long cnt;
long long merge_sort(long long s,long long e)
{
	if(s<e)
	{
		long long m=(s+e)/2;
		merge_sort(s,m);
		merge_sort(m+1,e);
		long long i=s,j=m+1;long long k=s;
		long long I=m-s+1;
		while(k<=e)
		{
			if((j>e)||(i<=m&&a[i]<=a[j]))
			{
				t[k++]=a[i++];
				I--;
			}
			else
			{
				t[k++]=a[j++];
				cnt+=I;
			}
		}
		for(long long i=s;i<=e;++i) 	a[i]=t[i];
	} 
	return 0;
}
int main()
{
	long long n,k;
	while(cin>>n>>k)
	{
		cnt=0;
		for(long long i=0;i<n;++i)	cin>>a[i];
		merge_sort(0,n-1);
		long long ans=cnt-k;
		if(ans>0)	cout<<ans<<endl;
		else	cout<<"0"<<endl;
	}
	return 0;
}
```

