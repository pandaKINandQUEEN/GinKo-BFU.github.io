---
layout:     post
title:      "排序输出"
subtitle:   "我的第一个set程序"
date:       2018-01-23
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    - SET
    - ACM
---

## 排序输出
这是第一次用set,这里利用了集合的互异性和set的自动排序，不然很容易TLE

set升序排列

### 描述
给你一些整数，请将它们排序后输出。

### 输入
输入首先包含一个正整数T(0<T<100)，表示测试数据组数。

接下来T组测试数据。

每组测试数据首先包含一个正整数m(m<=5000000),表示本组测试数据包含的数据个数,然后是m行,每行一个正整数n(n<=100000)

### 输出
对每组测试数据，请将所有数据排序后输出，为了简单一点，相同的数只需要输出一次，每个数据占一行。

### 样例输入1 
2<br>
3<br>
112<br>
111<br>
112<br>
6<br>
1<br>
12345<br>
98765<br>
12008<br>
12010<br>
2009<br>

### 样例输出1 
111<br>
112<br>
1<br>
2009<br>
12008<br>
12010<br>
12345<br>
98765

### AC
``` cpp
#include<iostream>

#include<algorithm>

#include<cstdio>

#include<set>

using namespace std;

int main()
{
	int T,t,n;
	scanf("%d",&T);
	while(T--)
	{
		set<int> s;
		scanf("%d",&n);
		for(int i=0;i<n;++i)
		{
			scanf("%d",&t);
			s.insert(t);
		}
		for(set<int>::iterator i=s.begin();i!=s.end();++i)
		{
			printf("%d\n",*i);
		}
	}
	return 0;
 }
```
