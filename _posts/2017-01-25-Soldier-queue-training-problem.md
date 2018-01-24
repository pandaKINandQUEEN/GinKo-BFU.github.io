---
layout:     post
title:      "士兵队列训练问题 "
subtitle:   ""
date:       2017-01-23
author:     "JinTao"
header-img: "img/bloghead.jpg"
catalog: true
tags:
    - queue
    - ACM
    
---

## 士兵队列训练问题 
这题第一次提交"Presentation Error"——格式错误
原来是最后一个数后面不能输出空格
还有这题要注意 "多个测试数据组"

### 描述
某部队进行新兵队列训练，将新兵从一开始按顺序依次编号，并排成一行横队，训练的规则如下：从头开始一至二报数，凡报到二的出列，剩下的向小序号方向靠拢，再从头开始进行一至三报数，凡报到三的出列，剩下的向小序号方向靠拢，继续从头开始进行一至二报数。。。，以后从头开始轮流进行一至二报数、一至三报数直到剩下的人数不超过三人为止。 

### 输入
本题有多个测试数据组，第一行为组数N，接着为N行新兵人数，新兵人数不超过5000。

### 输出
共有N行，分别对应输入的新兵人数，每行输出剩下的新兵最初的编号，编号之间有一个空格。
### 样例输入1 
2<br>
20<br>
40

### 样例输出1 
1 7 19<br>
1 19 37


``` cpp
#include<iostream>

#include<queue>

using namespace std;
queue<int>q;
queue<int>blank;
int size;
void ctrl(int n)
{
	int len=size;
	for(int i=1;i<=len;++i)
	{
		if(i%n!=0)
		{
			int t=q.front();
			q.push(t);
		}
		else
			size--;
		q.pop();
	}
}
int main()
{
	
		int N;
		while(cin>>N)
		{
			while(N--)
			{
				int n;cin>>n;
				size=0;int c=2;
				q=blank;
				for(int i=1;i<=n;++i)
				{
					q.push(i);size++;
				}
				while(size>3)
				{
					if(c%2==0)
					{
						ctrl(2);
					}
					else
					{
						ctrl(3);
					}
					c++;
				}
				cout<<q.front();q.pop();
				while(!q.empty())
				{
					cout<<" "<<q.front();q.pop();
				}
				cout<<endl;
			}
		}
	
	return 0;
}
```


