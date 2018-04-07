---
layout:     post
title:      "遍历二叉排序树"
subtitle:   ""
date:       2018-04-07
author:     "JinTao"
header-img: "img/Headers/racing.jpg"
catalog: true
tags:
- 二叉搜索树
- ACM
---

## 遍历二叉排序树

### 描述
二叉排序树，是指一棵空树或者具有下列性质的二叉树：

1.若任意节点的左子树不空，则左子树上所有结点的值均小于或等于它的根结点的值；

2.任意节点的右子树不空，则右子树上所有结点的值均大于它的根结点的值；

3.任意节点的左、右子树也分别为二叉查找树。

4.没有键值相等的节点

将一个无序序列插入二叉排序树中，就可以得到一个有序的序列。

往二叉排序树中插入的算法如下：

1.若b是空树，则将s所指结点作为根节点插入，否则：

2.若s->data小于等于b的根节点的数据域之值，则把s所指节点插入到左子树中，否则：

3.把s所指节点插入到右子树中。（新插入节点总是叶子节点）

例如无序数列8 3 10 1 6 4 7 14 13依次插入二叉树中，二叉树的结构应如下图所示：

给你一个数列，请将其插入二叉排序树中，再对这棵二叉排序树进行前序、中序、后序以及层次遍历，输出遍历结果。
![Binary Search Tree](http://jintao.space/img/Mat/BinarySearchTree.jpg)

### 输入
输入包含多组测试数据。
每组输入包含两行，第一行为一个整数N(1<N<100)，第二行为以空格分隔的N个整数。
### 输出
对于每一组输入数据，输出包括四行，分别为对构造的二叉排序树进行前序、中序、后序以及层次遍历的结果。遍历时，输出的每个整数后跟一个空格。
### 样例输入1 
9<br>
8 3 10 1 6 4 7 14 13
### 样例输出1 
8 3 1 6 4 7 10 14 13 <br>
1 3 4 6 7 8 10 13 14 <br>
1 4 7 6 3 13 14 10 8 <br>
8 3 10 1 6 14 4 7 13 

### EXP
完全二叉树用数组存写起来简单，但这道题最坏情况要开2^100的数组，所以还是指针写起来更稳，但还是担心没有delete会超内存<br>
还有就是要注意题目要求,左右子树是如何定义的<br>
这道题数据没那么坏，用数组，指针都能通过，但显然用指针写快很多

### 指针写法(1ms)
``` cpp
#include<iostream>

#include<queue>

using namespace std;

typedef struct TreeNode
{
	int num;
	TreeNode *left,*right;
}TreeNode,*Node;

queue<Node>q;
int N;

void CreatBinaryTree(Node &node,int cnt)
{
	if(cnt==N)
	{
		return ;
	}
	else
	{
		int data;
		scanf("%d",&data);
		if(node==NULL)
		{
			node=new TreeNode;
			node->num=data;
			node->left=NULL;
			node->right=NULL;
		}
		else
		{
			Node temp=node;
			Node sign;
			while(temp!=NULL)
			{
				sign=temp;
				if(temp->num>=data)
				{
					temp=temp->left;
				}
				else
				{
					temp=temp->right;
				}
			}
			if(sign->num>=data)
			{
				Node t=new TreeNode;
				t->left=NULL;
				t->right=NULL;
				t->num=data;
				sign->left=t;
			}
			else
			{
				Node t=new TreeNode;
				t->left=NULL;
				t->right=NULL;
				t->num=data;
				sign->right=t;	
			}
		
		}
		
		CreatBinaryTree(node,cnt+1);
	}
	
}

void PreOrderTraverse(Node node)
{
	if(node==NULL)
	{
		return ;
	}
	printf("%d ",node->num);
	PreOrderTraverse(node->left);
	PreOrderTraverse(node->right);
}

void MidOrderTraverse(Node node)
{
	if(node==NULL)
	{
		return ;
	}
	MidOrderTraverse(node->left);
	printf("%d ",node->num);
	MidOrderTraverse(node->right);
}

void LastOrderTraverse(Node node)
{
	if(node==NULL)
	{
		return ;
	}
	LastOrderTraverse(node->left);
	LastOrderTraverse(node->right);
	printf("%d ",node->num);
}

void LevelOrderTraverse()
{
	while(!q.empty())
	{
		Node temp=q.front();
		printf("%d ",temp->num);
		
		if(temp->left!=NULL)
			q.push(temp->left);
		if(temp->right!=NULL)
			q.push(temp->right);
		
		q.pop();
	}
}

int main()
{
	while(cin>>N)
	{
		Node node=NULL;
		CreatBinaryTree(node,0);
		PreOrderTraverse(node);cout<<endl;
		MidOrderTraverse(node);cout<<endl;
		LastOrderTraverse(node);cout<<endl;
		q.push(node);
		LevelOrderTraverse();cout<<endl;
	}

	return 0;
}
```

### 数组写法(12ms)
```cpp
#include<iostream>

#include<queue>

using namespace std;

int N;
queue<int>q;

struct TreeNode
{
	int data;
	bool bol;

	TreeNode()
	{
		bol=false;
	}
}Node[1000000];

void CreatBinaryTree(int node,int cnt)
{
	if(cnt==N)
	{
		return ;
	}
	else
	{
		int data;
		scanf("%d",&data);
		if(Node[node].bol==false)
		{
			Node[node].bol=true;
			Node[node].data=data;
		}
		else
		{
			int sign=node;
			while(Node[sign].bol!=false)
			{
				if(data<=Node[sign].data)
				{
					sign=2*sign;
				}
				else
				{
					sign=2*sign+1;
				}
			}
			Node[sign].bol=true;
			Node[sign].data=data;
		}
		CreatBinaryTree(node,cnt+1);
	}
}

void PreOrderTraverse(int node)
{
	if(Node[node].bol==false)
		return ;
	printf("%d ",Node[node].data);
	PreOrderTraverse(node*2);
	PreOrderTraverse(node*2+1);
}

void MidOrderTraverse(int node)
{
	if(Node[node].bol==false)
		return ;
	MidOrderTraverse(node*2);
	printf("%d ",Node[node].data);
	MidOrderTraverse(node*2+1);
}

void LastOrderTraverse(int node)
{
	if(Node[node].bol==false)
		return ;
	LastOrderTraverse(node*2);
	LastOrderTraverse(node*2+1);
	printf("%d ",Node[node].data);
}

void LevelOrderTraverse()
{
	while(!q.empty())
	{
		int t=q.front();
		printf("%d ",Node[t].data);
		if(Node[t*2].bol==true)
			q.push(t*2);
		if(Node[t*2+1].bol==true)
			q.push(t*2+1);
		
		q.pop();
	}
}

int main()
{
	while(cin>>N)
	{
		for(int i=0;i<100;++i)
			Node[i].bol=false;
		
		CreatBinaryTree(1,0);
		
		PreOrderTraverse(1);	printf("\n");
		MidOrderTraverse(1);	printf("\n");
		LastOrderTraverse(1);	printf("\n");

		q.push(1);
		LevelOrderTraverse();	printf("\n");
	}
	return 0;
} 
```

