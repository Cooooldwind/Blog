---
title: CooooldWind_の试炼历程 (5)
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

## 这里是[P1245](https://www.luogu.com.cn/problem/P1245)的题解

这道蓝题很水。

###### 广告：[博客食用更香](https://www.luogu.com.cn/blog/747369/ColdWind-Growing-5)

---

## 思路

查找，对号码，输出第一组（省时间免得TLE

## 代码深入解析（C++）

### 转义

```cpp
string num_turning(string a){
	//字母打进来，数字输出去 
	string b;
	for(int i = 0;i < a.size();i++){
		int sub = int(a[i]) - 32;
		if(65 <= sub && sub <= 67) b = b + "1";
		if(68 <= sub && sub <= 70) b = b + "2";
		if(71 <= sub && sub <= 73) b = b + "3";
		if(74 <= sub && sub <= 76) b = b + "4";
		if(77 <= sub && sub <= 78) b = b + "5";
		if(79 <= sub && sub <= 81) b = b + "6";
		if(82 <= sub && sub <= 84) b = b + "7";
		if(85 <= sub && sub <= 87) b = b + "8";
		if(88 <= sub && sub <= 90) b = b + "9";
	}
	return b;
}
```
这段代码是把输入的字符存到字典里面所需要的转义函数，不难理解，把英文转成数字。

### DFS

```cpp
void translating(int left){
	if(isFindout) return; //摆烂到底 
	if(left >= num_str.size()){
		//找到了，摆烂 
		output();
		isFindout++;
		return;
	}
	for(int i = 1;i <= n;i++) //遍历判断且继续 
		if(wordbook_code[i] == num_str.substr(left,wordbook_code[i].size())){
			codes[c_num++] = i;
			translating(left + wordbook_ans[i].size());
			if(isFindout) return;
		}
	//到头了，删除锚点 
	codes[c_num--] = 0;
	return;
}
```
主要的函数，就是DFS嘛（？

### 其它

```cpp
#include<bits/stdc++.h>
using namespace std;

string num_str,wordbook_code[110],wordbook_ans[110];
int n,c_num,isFindout,codes[5000000];

void output(){
	for(int i = 0;i < c_num - 1;i++)
		cout << wordbook_ans[codes[i]] << " ";
	cout << wordbook_ans[codes[c_num - 1]];
	return; 
}

int main(){
	cin >> n;
	cin >> num_str;
	for(int i = 1;i <= n;i++){
		//单词和代码的转义 
		cin >> wordbook_ans[i];
		wordbook_code[i] = num_turning(wordbook_ans[i]);
	}
	translating(0);
	if(!isFindout) cout << "No Solutions!";
	return 0;
}
```

其他的七七八八的东西包括输入和输出。

---

没了。

很多东西花点心思就能理解，注释也有提示的。

一天更两期真的累（T_T