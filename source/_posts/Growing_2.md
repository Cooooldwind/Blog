---
title: CooooldWind_の试炼历程 (2)
date: 2023-10-14 16:45:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
---

# 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 做个[P3955](https://www.luogu.com.cn/problem/P3955)。

###### 广告：[博客食用更香](https://www.luogu.com.cn/blog/747369/ColdWind-Growing-2)

---


### 思路

思路大概就是先把东西存起来（~~这不是废话？~~）

然后搞个很大（小）的数组

### 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

struct reader{
	int need;
	int l;
};

int main(){
	reader r[1010];
	int books[1010];
	int n,q;
	cin >> n >> q;
	for(int i = 0;i < n;i++)cin >> books[i];
	for(int i = 0;i < q;i++)cin >> r[i].l >> r[i].need;
	
	int m[8]={1,10,100,1000,10000,100000,1000000,10000000};
	sort(books,books + n);
	for(int i = 0; i < q;i++){
		int a = -1;
		for(int j = 0;j < n;j++){
			int g = books[j] % m[r[i].l];
			if(g == r[i].need){
				a = books[j] ;
				break;
			}
		}
		cout << a << endl;
	}
} 
```