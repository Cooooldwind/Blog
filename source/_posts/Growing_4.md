---
title: CooooldWind_の试炼历程 (4)
date: 2023-10-14 15:45:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
---

# 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 是的我又来了（

这里是[P1394](https://www.luogu.com.cn/problem/P1394)的题解。

当时做这题主要是因为是fj的（自豪

###### 广告：[博客食用更香](https://www.luogu.com.cn/blog/747369/ColdWind-Growing-4)

---

## 思路

输入并判断这水怎么流的，然后一个个去查能不能到就好了。

那就打个三重循环？？？

**为什么打三重循环**：有水能从不是起点的地方流到自己那里去（比如起点在8,8到5有路，5到3有路，那么8，5，3都有水）

```cpp
#include<bits/stdc++.h>
using namespace std;

int n,m,h[500],road[500][500];

int main(){
	cin >> n >> m;
	for(int i = 1;i <= n;i++) cin >> h[i];
	for(int i = 0;i < m;i++){
		int f,t;
		cin >> f >> t;
                //高处？低处？
		if(h[f] > h[t]) road[f][t] = 1;
		else if(h[t] > h[f]) road[t][f] = 1;
	}
	for(int i = 1;i <= n;i++){
		road[i][i] = 1;//水在自己家
		int judge = 0;
		for(int j = 1;j <= n;j++)
			for(int k = 1;k <= n;k++){
				if(road[k][j]){//有路，则为1
					judge++;
					break;
				}
			}		
		if(judge == n){
			cout << "Oui, j'ai trouve la solution." << endl << i;
			return 0;
		}
		road[i][i] = 0;
	}
	cout << "Non";
	return 0;
}
```