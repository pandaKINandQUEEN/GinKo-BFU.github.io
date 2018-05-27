---
layout:     post
title:      "人见人爱A^B"
subtitle:   ""
date:       2018-03-27
author:     "JinTao"
header-img: "img/lanqiao.jpg"
catalog: true
tags:
- 快速幂
---

## 人见人爱A^B

### 描述
求A^B的最后三位数表示的整数。

说明：A^B的含义是“A的B次方”
### 输入
求A^B的最后三位数表示的整数。

说明：A^B的含义是“A的B次方”
### 输出
输出一行：行李箱内物品的最大价值。
### 样例输入1 
2 3<br>
12 6<br>
6789 10000<br>
0 0

### 样例输出1 
8<br>
984<br>
1


### Exp
马上就蓝桥杯了，重温一下快速幂，万一···

### AC代码
``` cpp
#include<iostream>

using namespace std;
int qpow(int a,int b)
{
	int base=a;
	int ans=1;
	while(b)
	{
		ans%=1000;
		base%=1000;
		if(b&1)
		{
			ans*=base;
		}
		base*=base;
		b>>=1;
	}	
	return ans;
}
int main()
{
	int a,b;
	while((cin>>a>>b)&&(a+b)) 
	{
		cout<<qpow(a,b)%1000<<endl;
	}
	return 0;
}
```

