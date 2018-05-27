---
layout:     post
title:      "Matrix Power Series"
subtitle:   ""
date:       2018-04-04
author:     "JinTao"
header-img: "img/Headers/racing.jpg"
catalog: true
tags:
- 矩阵快速幂
---

## Matrix Power Series

### 描述
Given a n × n matrix A and a positive integer k, find the sum S = A + A2 + A3 + … + Ak.
### 输入
The input contains exactly one test case. The first line of input contains three positive integers n (n ≤ 30), k (k ≤ 109) and m (m < 104). Then follow n lines each containing n nonnegative integers below 32,768, giving A’s elements in row-major order.
### 输出
Output the elements of S modulo m in the same way as A is given.
### 样例输入1 
2 2 4<br>
0 1<br>
1 1
### 样例输出1 
1 2<br>
2 3


### AC代码
``` cpp
#include<iostream>

#include<cstring>

using namespace std;
int N, K, M;
class Matrix
{
public:
	int mat[35][35];
	Matrix()
	{
		memset(mat, 0, sizeof(mat));
	}
	Matrix(int s)
	{
		memset(mat, 0, sizeof(mat));
		
		for (int i = 0; i<N; ++i)
			mat[i][i] = s;
	}
	Matrix operator*(const Matrix &b);
	Matrix operator+(const Matrix &b);
};

Matrix Matrix::operator*(const Matrix &b)
{
	Matrix a(0);
	for (int i = 0; i<N; ++i)
	{
		for (int k = 0; k<N; ++k)
		{
			if (mat[i][k])
				for (int j = 0; j<N; ++j)
				{
					a.mat[i][j] += (mat[i][k] * b.mat[k][j])%M;
				}
		}
	}
	return a;
}

Matrix Matrix::operator+(const Matrix &b)
{
	Matrix a(0);
	for (int i = 0; i<N; ++i)
	{
		for (int j = 0; j<N; ++j)
		{
			a.mat[i][j] = (mat[i][j] + b.mat[i][j])%M;
		}
	}
	return a;
}

class MMatrix
{
public:
	Matrix mat[2][2];
	MMatrix operator*(const MMatrix &b);
};

MMatrix MMatrix::operator*(const MMatrix &b)
{
	Matrix O(0), U(1);
	MMatrix a;
	for (int i = 0; i<2; ++i)
	{
		for (int j = 0; j<2; ++j)
		{
			a.mat[i][j] = O;
		}
	}

	for (int i = 0; i<2; ++i)
	{
		for (int k = 0; k<2; ++k)
		{
			for (int j = 0; j<2; ++j)
			{
				a.mat[i][j] =a.mat[i][j] + mat[i][k] * b.mat[k][j];
			}
		}
	}
	return a;
}

MMatrix MMatrix_pow(MMatrix a, int k)
{
	MMatrix base = a;
	MMatrix ans = a;
	while (k)
	{
		if (k & 1)
		{
			ans = base*ans;
		}
		base = base*base;
		k >>= 1;
	}
	Matrix t(-1);
	ans.mat[0][1]=ans.mat[0][1]+t;
	return ans;
}

int main()
{
	cin >> N >> K >> M;
	Matrix A(0);
	for (int i = 0; i<N; ++i)
	{
		for (int j = 0; j<N; ++j)
		{
			scanf("%d", &A.mat[i][j]);
		}
	}
	Matrix U(1), O(0);
	MMatrix con;
	con.mat[0][0] = A; con.mat[0][1] = U; con.mat[1][0] = O; con.mat[1][1] = U;
	MMatrix ans = MMatrix_pow(con, K);
	for (int i = 0; i<N; ++i)
	{
		for (int j = 0; j<N; ++j)
		{
			if(ans.mat[0][1].mat[i][j]>=0)
				cout << ans.mat[0][1].mat[i][j] <<" ";
				else
				cout<< ans.mat[0][1].mat[i][j] +M<<" ";
		}
		cout << endl;
	}
	return 0;
}
```

