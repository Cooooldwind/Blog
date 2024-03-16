---
title: CooooldWind_の试炼历程 (3)
date: 2023-10-14 16:15:00
tags: 
- 题解
- CooooldWind_の试炼历程
mathjax: true
categories:
- 算法竞赛
---

## 欢迎来到CooooldWind_的试炼历程

本系列主要是讲自己在平常做题的时候的一些小花絮，但是已经托更很久了，趁着刚搞好GitHub Pages，今天把之前的都推下（外传就算了吧）。

## 这里是[P1750](https://www.luogu.com.cn/problem/P1750)的题解
### 想法

想法很简单，这不就是个栈？

但是有个点注意下，$10$行和$18$行建立待处理数组和栈的时候为什么用```long long```类型而不是朴实无华的```int```?

因为最大元素大小$2*10^9$，我怕超了（


###### 广告：[博客食用更香](https://www.luogu.com.cn/blog/747369/ColdWind-Growing-3)

------------


### 完整答案

```cpp
#include<bits/stdc++.h>
using namespace std;

long long nums[10000];
int n,c;

int main(){
	//输入 
	cin >> n >> c;
	for(int i = 0;i < n;i++) cin >> nums[i];
	int output = 0;
	stack<long long> s;
	int pos = 0;
	while(s.size() + output < n){
		int zone_lost =  c - s.size();
		int min_pos;
		long long minn = 2*10*10*10*10*10*10*10*10*10;//minn是2*10^9是因为元素大小最大就这么大 
		//最小值min_num所在的位置
		for(int r = pos;r < min(pos + zone_lost,n);r++){
			if(nums[r] < minn){
				minn = nums[r];
				min_pos = r;
			}
		} 
		long long min_num = nums[min_pos];
		if(s.empty() || s.top() > min_num){
			for(int i = pos;i <= min_pos;i++) s.push(nums[i]);
			pos = min(min_pos + 1,n - 1);
		}
		cout << s.top() << " ";
		s.pop();
		output++;
	}
	while(s.empty() == 0) {
		cout << s.top() << " ";
		s.pop();
	}
} 
```


------------
### 讲解
#### 定义和输入
```cpp
#include<bits/stdc++.h>
using namespace std;

long long nums[10000];
int n,c;

int main(){
	//输入 
	cin >> n >> c;
	for(int i = 0;i < n;i++) cin >> nums[i];
	int output = 0;
	stack<long long> s;
	int pos = 0;
```
就这里，$n$和$c$对应题目里面的$n$和$c$，$nums$是第二行的输入，$output$计算经过处理的数字量，$pos$指目前计算的位置。
#### while循环
```cpp
while(s.size() + output < n){
	int zone_lost =  c - s.size();
	int min_pos;
	long long minn = 2*1000000000;
	//最小值min_num所在的位置
	for(int r = pos;r < min(pos + zone_lost,n);r++){
		if(nums[r] < minn){
			minn = nums[r];
			min_pos = r;
		}
	} 
	long long min_num = nums[min_pos];
	if(s.empty() || s.top() > min_num){
		for(int i = pos;i <= min_pos;i++) s.push(nums[i]);
		pos = min(min_pos + 1,n - 1);
	}
	cout << s.top() << " ";
	s.pop();
	output++;
}
```
```zone_lost```就是占剩下多少位置，```s.size()```大家应该都会，就是s栈的大小。

里面的第一个for循环寻找待处理数组中前```zone_lost```位中最小的位置（就是能存进去的里面找最小的那个在哪）。

如果```pos+zone_lost```超了数组最大值的话那就不好了，所以为了检测它超了还是没超，得有```min(pos + zone_lost,n)```在for的判断里面出现。

底下的if就是一个个存到$s$，直到存到刚刚说的“能存进去的里面找最小的那个”的位置。

if底下的三行依次是输出、出栈、累加。

#### 底下的while循环
```cpp
while(s.empty() == 0) {
	cout << s.top() << " ";
	s.pop();
}
```
因为有时候栈不可能在数组里面的数处理完的时候完全空，所以写了while循环。


------------
### 自此这题就解完啦。
看起来不难，但其实还是有点深度。

**这个题解非常蒟蒻向，大佬们别喷。**

**~~蒟蒻写的题解有人点赞嘛？~~**