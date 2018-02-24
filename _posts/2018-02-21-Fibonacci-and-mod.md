---
layout:     post
title:      "入门训练 Fibonacci数列"
subtitle:   ""
date:       2018-02-21
author:     "JinTao"
header-img: "img/2018newyear.jpg"
catalog: true
tags:
- 蓝桥杯
---

## 入门训练 Fibonacci数列

### 描述
Fibonacci数列的递推公式为：Fn=Fn-1+Fn-2，其中F1=F2=1。
当n比较大时，Fn也非常大，现在我们想知道，Fn除以10007的余数是多少。
### 输入
输入包含一个整数n。1 <= n <= 1,000,000。
### 输出
输出一行，包含一个整数，表示Fn除以10007的余数。
### 样例输入1 
22

### 样例输出1 
7704
### Experience
二十天没敲代码已然是个废人..
看到n的规模竟然想到了高精度..
没那么复杂其实

(a+b)%c=(a%c+b%c)%c;

### AC
``` cpp
#include<iostream>

using namespace std;
int a[1000050];
int main()
{
	
	int n;cin>>n;
	a[1]=1;a[2]=1;
	for(int i=3;i<=n;++i)
	{
		a[i]=(a[i-1]+a[i-2])%10007;	
	}
	cout<<a[n]<<endl;
	return 0;	
} 
```

