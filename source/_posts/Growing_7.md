---
title: CooooldWind_の试炼历程 (7)
date: 2023-10-14 14:45:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
---

# 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 这里是[P1097](https://www.luogu.com.cn/problem/P1097)的题解

### 思路

排序，计数输出。

```cpp
#include<bits/stdc++.h>
int n,m,t[150000001];
int main(){
	std::cin >> n;
	for(int i = 0;i < n;i++) std::cin >> t[i];
	std::sort(t,t + n);//排序
	for(int i = 0;i < n;i++){
		int get = t[i],time = 1,j = i;
		while(t[i] == t[j]) j++;//计数，j是最后一个出现这数字的地方
		std::cout << get << " " << j - i << endl;
		i = j - 1;
	}
	return 0;
}
```

连namespace都压。

**14行搞定**此题。

(之前用结构体80分的是谁，我不说

(就是我