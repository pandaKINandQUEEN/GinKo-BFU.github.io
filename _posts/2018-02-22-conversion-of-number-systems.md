---
layout:     post
title:      "标准io进制转换"
subtitle:   ""
date:       2018-02-22
author:     "JinTao"
header-img: "img/2018newyear.jpg"
catalog: true
tags:
- ACM
- 蓝桥杯
---

## A + B
  做到蓝桥杯一些进制转换的题，突然就回忆起stdio就可以控制，动手做一下问题还挺多

## HDU 1720

### 描述
Many classmates said to me that A+B is must needs.
If you can’t AC this problem, you would invite me for night meal. ^_^
### 输入
Input may contain multiple test cases. Each case contains A and B in one line.
A, B are hexadecimal number.
Input terminates by EOF.
 
### 输出
Output A+B in decimal number in one line.
### 样例输入1 
1 9<br>
A B<br>
a b
### 样例输出1 
10<br>
21<br>
21

### AC
``` cpp
#include<iostream>

#include<cstdio>

using namespace std;
int main()
{
    int a,b;
    while(scanf("%x%x",&a,&b)!=EOF)
    {
        printf("%d\n",a+b);
    }
    return 0;
}
```

``` cpp
//这里要注意的是 用了%llx，a、b就要定义成 long long 不然测试样例输出为 9 11 11

#include<iostream>

#include<cstdio>

using namespace std;
int main()
{
    long long a,b;
    while(scanf("%llx %llx",&a,&b)!=EOF)
    {
        printf("%lld\n",a+b);
    }
    return 0;
}
```



## HDU 2057

### 描述
There must be many A + B problems in our HDOJ , now a new one is coming.
Give you two hexadecimal integers , your task is to calculate the sum of them,and print it in hexadecimal too.
Easy ? AC it !

### 输入
The input contains several test cases, please process to the end of the file.
Each case consists of two hexadecimal integers A and B in a line seperated by a blank.
The length of A and B is less than 15.
### 输出
For each test case,print the sum of A and B in hexadecimal in one line.
### 样例输入1 
+A -A<br>
+1A 12<br>
1A -9<br>
-1A -12<br>
1A -AA
### 样例输出1 
0<br>
2C<br>
11<br>
-2C<br>
-90

### Experience
这题%x应该是不够，得%llx。以后还是llx保险。%llx,%llX控制字母大小写。

一开始这样写的样例输出会出现fffffff之类，所以计算负数的时候要转化成十进制先算，如果十进制结果小于零就取相反数转16进制，多输出个符号就行

### AC
```cpp
#include<iostream>

#include <cstdio>

using namespace std;
int main()  
{  
    long long a, b, ans;  
  
    while(scanf("%llx %llx", &a, &b) != EOF) 
	{  
        ans = a + b;  
  
        if (ans >= 0)  
            printf("%llX\n", ans);  
        else  
            printf("-%llX\n", -ans);  
    }
    return 0;  
}
```

