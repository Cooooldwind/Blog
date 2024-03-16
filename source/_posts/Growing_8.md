---
title: CooooldWind_の试炼历程 (8)
date: 2023-10-14 14:45:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
categories:
- 算法竞赛
---

## 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 这里是[P8813](https://www.luogu.com.cn/problem/P8813)的题解

### 思路

模拟。有手题，不知道为什么会有人想用快速幂…（蒟蒻

### 答案

```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
	long long a,b,c = 1; cin >> a >> b;
	for(int i = 0;i < b;i++)
		if(c > 1000000000){
			cout << -1;
			return 0;
		}
		else c *= a;
	cout << c;
	return 0;
}
```

### 要点

#### #1：开long long

long long防爆的，最大是$2^6$$^4$。

#### #2：for里面加if

同样防爆。