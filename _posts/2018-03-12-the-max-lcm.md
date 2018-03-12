---
layout:     post
title:      "最大最小公倍数"
subtitle:   ""
date:       2018-03-12
author:     "JinTao"
header-img: "img/lanqiao.jpg"
catalog: true
tags:
- 蓝桥杯
- 贪心
---

## 最大最小公倍数

### 描述
已知一个正整数N，问从1~N中任选出三个数，他们的最小公倍数最大可以为多少。
### 输入
输入一个正整数N。1 <= N <= 10^6。
### 输出
输出一个整数，表示你找到的最小公倍数。
### 样例输入1 
9

### 样例输出1 
504


### Exp
只想说……妙啊<br>
首先确定是从大到小开始看，然后考虑到第一个数是奇数时，奇偶奇，其中两个奇数中间差2，但奇数没有因子2,n和n-2也不会有因子3。<br>
第一个数是偶数时，n,n-1,n-2是 偶奇偶，这时候两个偶数之间一定会有公共因子2，然后需要n-2再往后推一个取n-3，即n,n-1,n-3（偶奇奇）,
但这时候要注意，n，n-3之间可能会有公共因子3，<br>
这时候就需要判断n能否被3整除，如果可以，n-3也会被3整除，这样就不能取这三个数了，就不能再取n了，整体往后推一个，取n-1,n-2,n-3.

### AC代码
``` cpp
#include<iostream>

using namespace std;
int main()
{
	long long N,ans;cin>>N;
	if(N%2==1)
	{
		ans=N*(N-1)*(N-2);
	}
	else
	{
		if(N%3!=0)
		{
			ans=N*(N-1)*(N-3);
		}
		else
		{
			ans=(N-1)*(N-2)*(N-3);
		}
	}
	cout<<ans<<endl;
	return 0;
}
```

