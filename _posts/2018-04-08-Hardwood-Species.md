---
layout:     post
title:      "Hardwood Species"
subtitle:   ""
date:       2018-04-08
author:     "JinTao"
header-img: "img/Headers/racing.jpg"
catalog: true
tags:
- 二叉搜索树
- ACM
---

## Hardwood Species

### 描述
POJ2418,题目大意是输入若干单词，可能会有重复，统计每个单词出现次数所占总数的百分比，并按字典序输出
### 输入
Input to your program consists of a list of the species of every tree observed by the satellite; one tree per line. No species name exceeds 30 characters. There are no more than 10,000 species and no more than 1,000,000 trees.
### 输出
Print the name of each species represented in the population, in alphabetical order, followed by the percentage of the population it represents, to 4 decimal places.
### 样例输入1 
Red Alder<br>
Ash<br>
Aspen<br>
Basswood<br>
Ash<br>
Beech<br>
Yellow Birch<br>
Ash<br>
Cherry<br>
Cottonwood<br>
Ash<br>
Cypress<br>
Red Elm<br>
Gum<br>
Hackberry<br>
White Oak<br>
Hickory<br>
Pecan<br>
Hard Maple<br>
White Oak<br>
Soft Maple<br>
Red Oak<br>
Red Oak<br>
White Oak<br>
Poplan<br>
Sassafras<br>
Sycamore<br>
Black Walnut<br>
Willow
### 样例输出1 
Ash 13.7931<br>
Aspen 3.4483<br>
Basswood 3.4483<br>
Beech 3.4483<br>
Black Walnut 3.4483<br>
Cherry 3.4483<br>
Cottonwood 3.4483<br>
Cypress 3.4483<br>
Gum 3.4483<br>
Hackberry 3.4483<br>
Hard Maple 3.4483<br>
Hickory 3.4483<br>
Pecan 3.4483<br>
Poplan 3.4483<br>
Red Alder 3.4483<br>
Red Elm 3.4483<br>
Red Oak 6.8966<br>
Sassafras 3.4483<br>
Soft Maple 3.4483<br>
Sycamore 3.4483<br>
White Oak 10.3448<br>
Willow 3.4483<br>
Yellow Birch 3.4483

### EXP
这题限时10000ms,用map也能水过,但性能还是自己写的好些。<br>
这也算是自主完成的第一棵查找树了,还是遇到了一些问题：<br>
  每次new一个新节点后注意别忘把left,right指针赋值为NULL<br>
  题目要求字典序输出，用中序遍历。<br>
  map用getline的时候头文件还要加#include<string>,否则编译出错<br>
  ctrl+z结束输入

### map水过(420K 3110MS)
``` cpp
#include<cstring>

#include<iostream>

#include<string>

#include<map>

using namespace std;
double n=0;
int main()
{
	string s;
	map<string,int>mapp;
	while(getline(cin,s))
	{
		mapp[s]++;
		n++;
	}
	map<string,int>::iterator it;
	for(it=mapp.begin();it!=mapp.end();it++)
	{
		cout<<it->first<<" ";
		double ans=it->second/n*100.0;
		printf("%.4lf\n",ans);
	}
	return 0;
}
```

### 手写BST(364K 1266MS)
```cpp
#include<iostream>

#include<cstring>

using namespace std;
double n=0;
struct TreeNode
{
	char s[31];
	int cnt;
	TreeNode *left,*right;
};
void insertBST(char *s,TreeNode * &node)
{
	if(node==NULL)
	{
		node=new TreeNode;
		node->left=NULL;
		node->right=NULL;
		strcpy(node->s,s);
		node->cnt=1;
	}
	else
	{
		if(strcmp(s,node->s)==0)
		{
			node->cnt+=1;
		}
		else if(strcmp(s,node->s)<0)
		{
			insertBST(s,node->left);
		}
		else
		{
			insertBST(s,node->right); 
		}
	}
}

void MidOrderTraverse(TreeNode * node)
{
	if(node==NULL)
	{
		return ;	
	}
	MidOrderTraverse(node->left);
	printf("%s %.4lf\n",node->s,(node->cnt)/n*100.0);
	MidOrderTraverse(node->right);
}


int main()
{
	char s[31];
	TreeNode *node=NULL;
	while(gets(s)!=NULL)
	{
		insertBST(s,node);
		n+=1;
	}
	MidOrderTraverse(node);
	return 0;
}
```

