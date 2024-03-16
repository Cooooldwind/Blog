---
title: CooooldWind_の试炼历程 (1)
date: 2023-10-14 17:15:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
categories:
- 算法竞赛
---

## 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 这里是[P2615](https://www.luogu.com.cn/problem/P2615)的题解

### 废话

今天挑战P2615属实被难住了（毕竟是个萌新）
然后想了点想法做了出来

### 思路&代码

#### 初始化

```cpp
int n;
cin >> n;
int block[50][50] = {5000};
for(int i = 1;i <= n;i++)
	for(int j = 1;j <= n;j++)
		block[i][j] = 0;
block[1][(n + 1) / 2] = 1;
```
这一段是初始化，因为懒得再坐标-1了，而且调试时发现外框不设置成一个奇怪的数就会有问题，所以把第$0$行和第$0$列设成了$5000$，即$50\times50\times2$。

#### 模拟

然后是模拟。差点没看反行和列。
```cpp
for(int k = 2;k <= n * n;k++){
	int finding = k - 1;
	for(int i = 1;i <= n;i++){//行 
		for(int j = 1;j <= n;j++){//列 
			if(block[i][j] == finding){
				//若 (K-1) 在第一行但不在最后一列，则将K填在最后一行，(K-1) 所在列的右一列；
				if(i == 1 && j != n)
					block[n][j + 1] = k;
				
				//若 (K-1) 在最后一列但不在第一行，则将K填在第一列，(K-1) 所在行的上一行；
				if(i != 1 && j == n)
					block[i - 1][1] = k;
				
				//若 (K-1) 在第一行最后一列，则将K填在 (K-1) 的正下方；
				if(i == 1 && j == n)
					block[2][j] = k;
				
				//若 (K-1) 既不在第一行，也不在最后一列，如果 (K-1) 的右上方还未填数，则将 K 填在 (K-1) 的右上方，
				//否则将 K 填在 (K-1) 的正下方。
				if(i != 1 && j != n)
					if(block[i - 1][j + 1] == 0)
						block[i - 1][j + 1] = k;
					else
						block[i + 1][j] = k;
			} 
		}
	}
}

```
#### 输出
```cpp
for(int i = 1;i <= n;i++){//行 
	for(int j = 1;j <= n;j++){//列 
		cout << block[i][j] << " ";	
	}
	cout << endl;
}
```
### 再次废话
**本解法非最优题解，~~但应该是最绕的~~**