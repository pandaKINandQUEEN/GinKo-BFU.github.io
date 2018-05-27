---
layout:     post
title:      "入门训练 圆的面积"
subtitle:   ""
date:       2018-02-21
author:     "JinTao"
header-img: "img/2018newyear.jpg"
catalog: true
tags:
---

## 入门训练 圆的面积

### 描述
给定圆的半径r，求圆的面积。 1 <= r <= 10000
### 输入
输入包含一个整数r，表示圆的半径。 
### 输出
输出一行，包含一个实数，四舍五入保留小数点后7位，表示圆的面积。 
说明：在本题中，输入是一个整数，但是输出是一个实数。
对于实数输出的问题，请一定看清楚实数输出的要求，比如本题中要求保留小数点后7位，则你的程序必须严格的输出7位小数，输出过多或者过少的小数位数都是不行的，都会被认为错误。
实数输出的问题如果没有特别说明，舍入都是按四舍五入进行。
### 样例输入1 
4

### 样例输出1 
50.2654825 
### Experience
又一道水题，就是想说这道题对π的精度要求比较高，所以

tan(π/4)=1 --> atan(1.0)=PI;  头文件cmath
### AC
``` cpp
#include<iostream>

#include<cstdio>

#include<cmath>

using namespace std;
int main()
{
	double PI=atan(1.0)*4;
	double r;cin>>r;
	double ans=r*r*PI;
	printf("%.7lf\n",ans);
	return 0;
}
```

