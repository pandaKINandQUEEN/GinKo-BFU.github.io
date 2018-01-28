---
layout:     post
title:      "Sagheer and Nubian Market"
subtitle:   ""
date:       2018-01-28
author:     "JinTao"
header-img: "img/head2.jpg"
catalog: true
tags:
- ACM
- 二分
- 贪心
---

## Sagheer and Nubian Market
A掉这道题才明白什么叫做二分答案。这题的二分还有特殊之处，要控制好。

理解题意就走了不少弯路我的天，还有这题的测试压力有点大，最后干脆全改成Long Long才AC


### 描述
On his trip to Luxor and Aswan, Sagheer went to a Nubian market to buy some souvenirs for his friends and relatives. The market has some strange rules. It contains n different items numbered from 1 to n. The i-th item has base cost ai Egyptian pounds. If Sagheer buys k items with indices x1, x2, ..., xk, then the cost of item xj is axj + xj·k for 1 ≤ j ≤ k. In other words, the cost of an item is equal to its base cost in addition to its index multiplied by the factor k.

Sagheer wants to buy as many souvenirs as possible without paying more than S Egyptian pounds. Note that he cannot buy a souvenir more than once. If there are many ways to maximize the number of souvenirs, he will choose the way that will minimize the total cost. Can you help him with this task?
### 输入
The first line contains two integers n and S (1 ≤ n ≤ 105 and 1 ≤ S ≤ 109) — the number of souvenirs in the market and Sagheer's budget.

The second line contains n space-separated integers a1, a2, ..., an (1 ≤ ai ≤ 105) — the base costs of the souvenirs.


### 输出
On a single line, print two integers k, T — the maximum number of souvenirs Sagheer can buy and the minimum total cost to buy these k souvenirs.

### 样例输入1
3 11<br>
2 3 5

### 样例输出1 
2 11

### AC
``` cpp
#include<iostream>

#include<algorithm>

using namespace std;
long long a[100005],b[100005];
int main()
{
	long long n,s;	long long sum=0;
	while(cin>>n>>s)
	{
		a[0]=0;b[0]=0;long long ans=0;
		for(int i=1;i<=n;++i)	cin>>a[i];
		long long lef=0,rit=n;
		while(lef<rit)
		{
			long long m=(lef+rit+1)/2;//偏右取mid 
			sum=0;
			for(int i=0;i<=n;++i)	b[i]=a[i]+i*m;
			sort(b+0,b+n+1);
			for(int i=0;i<=m;++i)	sum+=b[i];
			if(sum<=s)	lef=m;//左边界不释放 
			else	rit=m-1;//只要不满足条件右侧向左侧收缩 
		}
		for(int i=0;i<=n;++i)	b[i]=a[i]+i*lef;
		sort(b+0,b+n+1);
		for(int i=0;i<=lef;++i) ans+=b[i];	
		cout<<lef<<" "<<ans<<endl;
	}
	return 0;
}
```



