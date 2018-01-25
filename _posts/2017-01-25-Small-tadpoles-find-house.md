---
layout:     post
title:      "小蝌蚪安家"
subtitle:   ""
date:       2017-01-25
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    - BFS
    - DFS
    - ACM
---

## 小蝌蚪安家


### 描述
在一个矩形区域内，有些地方有水，有些地方没水。所有相邻的有水的地方会共同组成一个水洼，小蝌蚪想在这块区域中找到一个最大的水洼来安家。（横竖算是联通，斜着的'.'不算联通）
### 输入
有多组输入数据，每组第一行包含两个正整数n，m（n，m<=100），接下来n行，每行m个字符，“.”表示有水，“#”表示没水。

### 输出
对于每组输入数据输出一行，包含一个整数，表示最大的水洼的面积。

### 样例输入1 
3 3<br>
##.<br>
#.#<br>
#.#

### 样例输出1 
2

#### dfs解法
``` cpp
#include<iostream>

using namespace std;
int x[4]={-1,0,1,0};
int y[4]={0,1,0,-1};
char map[105][105];
int maxx=-1;
int tmax=0;
int m,n;
void search(int u,int v);
int main()
{
	while(cin>>m>>n)
	{
		maxx=0;tmax=0;
		for(int i=0;i<m;++i)
			for(int j=0;j<n;++j)
			{
				cin>>map[i][j];
			}
		for(int i=0;i<m;++i)
			for(int j=0;j<n;++j)
			{
				if(map[i][j]=='.')
				{
					tmax=1;map[i][j]='#';
					search(i,j);
					if(tmax>maxx)
					{
						maxx=tmax;
					}
				}
			}
		cout<<maxx<<endl;
	}
	return 0;
}
void search(int u,int v)
{
	for(int i=0;i<4;++i)
	{
		if((u+x[i]>=0)&&(u+x[i]<m)&&(v+y[i]>=0)&&(v+y[i]<n))
		{
			if(map[u+x[i]][v+y[i]]=='.')
			{
				tmax+=1;map[u+x[i]][v+y[i]]='#';
				search(u+x[i],v+y[i]);
			}
		}
	}
}
```
#### bfs解法
```cpp
#include<iostream>

#include<cstring>

#include<string>

#include<queue>

#include<vector>

#include<algorithm>

using namespace std;
char map[101][101];
int x[4] = { -1,0,1,0 };
int y[4] = { 0,1,0,-1 };
int n, m;
void search();
vector <int> area;
int tempnum;
struct point
{
	int x, y;
};
queue <point> p;
queue <point> blank;
int main()
{
	while (cin >> n >> m)
	{
		point a;
		for(int i=0;i<n;++i)
			for (int j = 0; j < m; ++j)
			{
				cin >> map[i][j];
			}
		for(int i=0;i<n;++i)
			for (int j = 0; j < m; ++j)
			{
				if (map[i][j] == '.')
				{
					p = blank;
					tempnum =1;
					a.x = i; a.y = j;
					map[i][j] = '#';
					p.push(a);
					search();
					area.push_back(tempnum);
				}
			}
		sort(area.begin(), area.end());
		printf("%d\n", area[area.size()-1]);
		area.clear();
	}
	return 0;
}
void search()
{
	point temp;
	while (!p.empty())
	{
		temp = p.front();
		for (int i = 0; i < 4; ++i)
		{
			if ((temp.x + x[i] >= 0) && (temp.x + x[i] < n)
				&& (temp.y + y[i] >= 0) && (temp.y + y[i] < m)
				&& (map[temp.x + x[i]][temp.y + y[i]] == '.'))
			{
				point temp2;
				tempnum += 1;
				map[temp.x + x[i]][temp.y + y[i]] = '#';
				temp2.x = temp.x + x[i];
				temp2.y = temp.y + y[i];
				p.push(temp2);
			}
		}
		p.pop();
	}
}
```

