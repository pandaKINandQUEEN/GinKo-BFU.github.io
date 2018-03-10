---
layout:     post
title:      "The Traveling Judges Problem"
subtitle:   ""
date:       2018-03-10
author:     "JinTao"
header-img: "img/lanqiao.jpg"
catalog: true
tags:
- 蓝桥杯
- MST
- Prim
---

## The Traveling Judges Problem

### 描述
一组人要担任在一个特定城市举办的比赛的评委，他们需要找到最便宜的租车方式使得每个人都到达目标城市。他们观察发现，如果几个人在旅途的某一段坐同一辆租的车，就可以减少总费用。你的任务就是找出这些人应该采取的路线使得租车的总费用最小。
　　我们假定：
　　1. 租一辆车的费用与它行驶的距离成正比，没有燃油、保险、乘客人数多于一个等产生的额外费用。
　　2. 所有车的费用与行驶距离的比例相同。
　　3. 一辆车可以容纳任意数量的乘客。
　　4. 任意一对城市之间最多只有一条道路直接相连，每条道路都是双向的且长度大于0。
　　5. 每个人的起始城市到目标城市都至少有一种路线。
　　6. 若多个人的路线中经过同一城市，则这些人从该城市到目标城市必乘同一辆车。
　　7. 一个人可以乘一辆车到某个城市，再乘另一辆车离开该城市。
### 输入
第一行包含三个整数nc, dc和nr，表示地图上的城市个数，目标城市的编号和地图上的道路条数。
　　接下来nr行每行包含三个整数c1, c2和dist，表示一条长度为dist的双向道路(c1, c2)。
　　接下来一行包含一个整数nj，表示人数。
　　接下来一行包含nj个整数，表示每个人的起始城市。
  对于30%的数据，1 <= nc <= 8。
　　对于100%的数据，1 <= nc <= 20，1 <= nj <= 10，1 <= dist <= 100。
### 输出
第一行包含“distance = ”和一个整数，表示所租的车行驶的最小总距离。
　　接下来nj行每行包含一个人的访问路线，城市按访问顺序给出并用“-”连接。
　　存在多种方案时，选择需要访问到的城市集合元素最少的一种；仍然存在多种方案时，选择集合元素升序排列后字典序最小的一种。
### 样例输入1 
5 3 5<br>
1 2 1<br>
2 3 2<br>
3 4 3<br>
4 5 1<br>
2 4 2<br>
2<br>
5 1

### 样例输出1 
distance = 6<br>
5-4-2-3<br>
1-2-3

### 样例输入2
4 4 3<br>
1 3 1<br>
2 3 2<br>
3 4 2<br>
2<br>
1 2

### 样例输出2
distance = 5<br>
1-3-4<br>
2-3-4

### 样例输入3
3 3 3<br>
1 2 2<br>
1 3 3<br>
2 3 1<br>
2<br>
2 1

### 样例输出3
distance = 3<br>
2-3<br>
1-2-3
### Exp
第一次写最小生成树，这个代码还挺了不起的

鸣谢：ZYQ LYB 

CSDN[算法导论--最小生成树（Kruskal和Prim算法）](http://blog.csdn.net/luoshixian099/article/details/51908175)

### AC
``` cpp
#include<iostream>

#include<cstring>

using namespace std;

const int MaxC=20;
const int MaxJ=10;
int NC,DC,T=0,ans,NJ,best_map,mmin,sum;
int road[MaxC][MaxC],judges[MaxJ],fa[MaxC];

bool init()
{
	cin>>NC;

	cin>>DC; DC--;
	T = T | (1<<DC);
	memset(road,0,sizeof(road));
	ans=INT_MAX;
	int NR;cin>>NR;
	int c1,c2;
	for(int i=0;i<NR;++i)
	{
		cin>>c1>>c2;
		c1--; c2--;
		cin>>road[c1][c2];
		road[c2][c1]=road[c1][c2];
	}
	cin>>NJ;
	for(int i=0;i<NJ;++i)
	{
		cin>>judges[i]; judges[i]--;
		T = T | (1<<judges[i]);
	}
	return true;
}

void check(int map)
{
	int k;
	int d[MaxC];
	for(int i=0;i<MaxC;++i)	d[i]=-2;
	d[DC]=-1;
	for(int i=0;i<MaxC;++i)
	{
		if((map&1<<i)&&road[DC][i])	
		{
			d[i]=road[DC][i];
			fa[i]=DC;
		}
	}
	sum=0;

	while(1)
	{
		mmin=INT_MAX;
		for(int i=0;i<MaxC;++i)
		{
			if(d[i]>0&&d[i]<mmin)
			{
				mmin=d[i];
				k=i;
			}
		}

		if(mmin==INT_MAX)	break;
		
		sum+=mmin; d[k]=-1;

		for(int i=0;i<MaxC;++i)
		{
			if(((1<<i)&map)&&road[k][i])
			{
				if(d[i]==-2||d[i]>road[k][i])
				{
					d[i]=road[k][i];
					fa[i]=k;
				}
			}
		}
	}
	
	for(int i=0;i<MaxC;++i)
	{
		if((map&(1<<i))&&d[i]==-2)	return;	
	}
	
	if(sum<ans)
	{
		ans=sum;
		best_map=map;
	}
	else if(sum==ans)
	{
		int cnt0=0,cnt1=0;
		for(int i=0;i<MaxC;i++)
		{
			if(best_map&(1<<i)) cnt0++;
			if(map&(1<<i)) cnt1++;
		}
		if(cnt1<cnt0)
		{
			ans=sum;
			best_map=map;
			return;
		}
		if(cnt1>cnt0) return;
		
		for(int i=0;i<MaxC;++i)
		{
			if((best_map&(1<<i))&&!(map&(1<<i))) return;
			if(!(best_map&(1<<i))&&(map&(1<<i)))
			{
				ans=sum;
				best_map=map;
				return;
			}
		}	
	}
	
 return;
}

int main()
{
	best_map=0;
	
	init();
	
	for(int map=0;map<(1<<NC);map++)
	{
		if((map&T)==T)	check(map);
	}
	cout<<"distance = "<<ans<<endl;	
	check(best_map);
	

	
	for(int i=0;i<NJ;++i)
	{
		int temp=judges[i];
		while(temp!=DC)
		{
			cout<<temp+1<<"-";
			temp=fa[temp];
		}
		cout<<temp+1<<endl;
	}
	return 0;
} 

```

