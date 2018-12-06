---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem minm-loss         # 标题 
subtitle:   STL set和binary search的使用
date:       2018-12-5             # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/minimum-loss/problem'> 看题目戳我 </a>


## 题解思路
考虑在第$i$天卖出，只需要找到前面不小于该房价最小的那个。初次想法是用堆，但是这是不太可行的。因为维护这个堆花的时间不确定。若想保证$log$级别的查询和维护，平衡树是很棒的呀。这时候就要用到C++ STL set，它是基于红黑树实现的，自动排序。排好序用二分查找简直不要太舒服。

## 代码
    
    #include <bits/stdc++.h>

    using namespace std;

    int main()
    {
    int n;
    cin>>n;
    set<long long> s;
    long long tmp,minm=1e16;
    cin>>tmp;
    s.insert(tmp);
    for(int i=1;i<n;i++)
    {
        cin>>tmp;
        auto it=s.upper_bound(tmp);
        if(it != s.end()) minm = min(minm,*it - tmp);
        s.insert(tmp);
    }
    cout<<minm;
    return 0;
    
    }

