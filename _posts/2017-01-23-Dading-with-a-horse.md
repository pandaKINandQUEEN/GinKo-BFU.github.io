---
layout:     post
title:      "大钉骑马走江湖"
subtitle:   ""
date:       2017-01-23
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    - BFS
    - ACM
---

## 大钉骑马走江湖

### 描述
江湖是什么，对于在象棋界厮杀的大钉来说，江湖就是一个矩阵，他的目标，就是在江湖之中骑着马，从他的位置出发，走到终点。
当然，大钉的马也遵从中国象棋中的“马走日”的规则，而且在矩阵中，也会有一些障碍物，马不能跳到障碍物上；如果大钉的马面前有障碍物，即被“别马腿”，那么他将不能跳向有障碍物的左前和右前这两个方向。
请问最少需要多少步，大钉才能骑着马跳到终点。

### 输入
有多组测试样例。

每组第一行有两个数 n 和 m，代表矩阵的行数和列数，2 <= n <= m < 100。

接下来输入 n 行的字符串，其中 's' 代表起点，'e' 代表终点，'.'代表空地，'#'代表障碍物。

### 输出
对应每组输入，输出骑马跳到终点的最小步数，如果跳不到终点，输出 -1。

### 样例输入1 
3 3<br>
s..<br>
...<br>
..e<br>

3 3<br>
s#.<br>
...<br>
#.e<br>

### 样例输出1 
4<br>
-1

``` cpp
#include<iostream>

#include<cstdio>

#include<cstring>

#include<string>

#include<queue>

int q[8] = { -2,-1,1,2,2,1,-1,-2 };//p,q控制前进

int p[8] = { 1,2,2,1,-1,-2,-2,-1 };

int x[8] = { -1,0,0,1,1,0,0,-1 };//x,y控制蹩马腿

int y[8] = { 0,1,1,0,0,-1,-1,0 };
char map[101][101];
int sign[101][101];
int x2, y2;
int flag = 0;
int n, m;
using namespace std;
struct point
{
	int x, y, step;
};
void search();
queue <point> f;
queue <point> blank;
int main()
{
	while (cin >> n >> m)
	{
		memset(sign, 0, sizeof(sign));
		f = blank;
		flag = 0;
		for(int i=0;i<n;++i)
			for (int j = 0; j < m;++j)
			{
				cin >> map[i][j];
				if (map[i][j] == 's')
				{
					point temp;
					temp.x = i; temp.y = j; temp.step = 0;
					f.push(temp);
				}
				if (map[i][j] == 'e')
				{
					x2 = i; y2 = j;
				}
			}
		search();
		if (flag == 0)
		{
			printf("-1\n");
		}
	}
	return 0;
}
void search()
{
	while (!f.empty())
	{
		point temp;
		temp = f.front();
		if ((temp.x == x2) && (temp.y == y2))
		{
			printf("%d\n", temp.step);
			flag = 1;
			break;
		}
		point temp2;
		for (int i = 0; i < 8; ++i)
		{
			temp2.x = temp.x + q[i];
			temp2.y = temp.y + p[i];
			temp2.step = temp.step + 1;
			if ((temp2.x >= 0) && (temp2.x < n) && (temp2.y >= 0) && (temp2.y < m))
			{
				if ((map[temp2.x][temp2.y] != '#') && (sign[temp2.x][temp2.y] != 1))
				{
					if (map[temp.x + x[i]][temp.y + y[i]] != '#')
					{
						f.push(temp2);
						sign[temp2.x][temp2.y] = 1;
					}
				}
			}
		}
		f.pop();
	}
}
```
