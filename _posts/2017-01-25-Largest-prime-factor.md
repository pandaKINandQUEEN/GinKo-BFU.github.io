---
layout:     post
title:      "Largest prime factor"
subtitle:   ""
date:       2017-01-25
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    
    - 素筛
    - ACM
    
---

## Largest prime factor  
这应该是今天最开心的一次AC了，为了这道题自己曾想了好久。设计过好多自认为更优的算法。
其实在现在看来面对一道T掉的题，复杂度优化2倍甚至10倍有时都是不值一提的；
今天边A题边听了素筛算法，还自认为懂了（这不就跟我最初设计的差不多么~）。
结果在T掉之后会长又和我讲了一次素筛。

挖草！

原来is_prime()都不！需！要！；

突然发现emmmmmmm....我还是聪明哒…… ^ ^

最后注意！在用了素筛之后这题还是会T!原因是要用标准输入！！
### 描述
Everybody knows any number can be combined by the prime number. 
Now, your task is telling me what position of the largest prime factor. 
The position of prime 2 is 1, prime 3 is 2, and prime 5 is 3, etc. 
Specially, LPF(1) = 0. 

### 输入
Each line will contain one integer n(0 < n < 1000000). 

### 输出
Output the LPF(n). 
### 样例输入1 
1<br>
2<br>
3<br>
4<br>
5

### 样例输出1 
0<br>
1<br>
2<br>
1<br>
3


``` cpp
#include<iostream>

#include<cstring>

using namespace std;
int a[1000005];
int main()
{
	memset(a,0,sizeof(a));
	int cnt=0;
	for(int i=2;i<1000005;++i)
	{
		if(!a[i])
		{
				cnt++;
				for(int j=i;j<1000005;j+=i)
				{
					a[j]=cnt;
				}
		}	
	}
	int n;
	while(scanf("%d",&n)!=EOF)
	{
		cout<<a[n]<<endl;
	}
	return 0;
}
```



