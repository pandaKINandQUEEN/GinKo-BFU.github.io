---
layout:     post
title:      "连号区间数"
subtitle:   ""
date:       2018-03-14
author:     "JinTao"
header-img: "img/lanqiao.jpg"
catalog: true
tags:
---

## 连号区间数

### 描述
小明这些天一直在思考这样一个奇怪而有趣的问题：
在1~N的某个全排列中有多少个连号区间呢？这里所说的连号区间的定义是：
如果区间[L, R] 里的所有元素（即此排列的第L个到第R个元素）递增排序后能得到一个长度为R-L+1的“连续”数列，则称这个区间连号区间。
当N很小的时候，小明可以很快地算出答案，但是当N变大的时候，问题就不是那么简单了，现在小明需要你的帮助。
### 输入
第一行是一个正整数N (1 <= N <= 50000), 表示全排列的规模。
第二行是N个不同的数字Pi(1 <= Pi <= N)， 表示这N个数字的某一全排列。
### 输出
输出一个整数，表示不同连号区间的数目。
### 样例输入1 
4<br>
3 2 4 1

### 样例输出1 
7
### 样例输入2
5<br>
3 4 2 5 1
### 样例输出2
9

### Exp
多刷刷水题……经常会在水题上也纠结策略。<br>
对于区间[i,j],如果是连续区间则 区间max-区间min==j-i;

### AC代码
``` cpp
#include<iostream>

using namespace std;
int main()
{
	int a[500005];
	int n;scanf("%d",&n);
	int cnt=0;
	for(int i=0;i<n;++i)
	{
		scanf("%d",&a[i]);
	}
	
	for(int i=0;i<n;++i)
	{
		int mmax=a[i];
		int mmin=a[i];
		for(int j=i;j<n;++j)
		{
			mmax=max(mmax,a[j]);
			mmin=min(mmin,a[j]);
			if((mmax-mmin)==(j-i))
			{
				cnt++;
			}
		}
	}
	cout<<cnt<<endl;
	return 0;
}
```

