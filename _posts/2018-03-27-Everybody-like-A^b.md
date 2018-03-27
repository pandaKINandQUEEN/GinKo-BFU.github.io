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
- ACM
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
#include<cstring>
using namespace std;
int main()
{
	int m,n;
	while(cin>>n>>m)
	{
		int w[n+1],v[n+1];
		for(int i=1;i<=n;++i)
		{
			cin>>w[i]>>v[i];
		}
		
		int b[m+1];
		memset(b,0,sizeof(b));
		
		for(int I=1;I<=n;++I)
		{
			for(int i=m;i>=0;i--)
			{
				if(i>=w[I])
				{
					b[i]=max(b[i],b[i-w[I]]+v[I]);
				}
			}
		}
		cout<<b[m]<<endl;
	}
	return 0;
}
```

