---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Ants           # 标题 
subtitle:   
date:       2018-12-3              # 时间
author:     An automatic pencil                      # 作者
header-img: img/HackerRank-Ants.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:       HackerRank                        #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/ants/problem'> 看题目戳我 </a>

## 注意事项
* 蚂蚁初始位置都是整数
* 最终统计的是每个蚂蚁的次数， 不是相遇次数
* 每个蚂蚁初始位置不同

## 题解思路
到手这个题目，一头雾水。但是仔细一看，每个蚂蚁除了初始位置不同，剩余所有的东西都是相同的。而这个题目最烦的地方就是两个蚂蚁相遇后互相掉头，其实这个和两个蚂蚁不掉头穿过对方是相同的。因为这个操作就相当于换了一下两个蚂蚁的名字，而这个对于最终结果是没有影响的。如下图：

<div  align="center">    
    <img src="https://s1.ax1x.com/2018/12/03/FKRdJI.png" width = "50%" height = "50%" alt="图像无法显示" />
</div>

A和B会在C点相遇，按题目要求A和B在C点会掉头。如果不掉头那么其实就是A和B换了一下名字。这还是那群蚂蚁，整体位置状态没有变化，也就对结果没什么影响。那这个问题最烦人的地方就没了，所有蚂蚁都是一直按原方向走就可以了。
然后看给定的秒数，每个蚂蚁要走$\frac{10^9*0.1}{1000}=10^5$圈，外加每个蚂蚁走0.6。先考虑整圈的情况，走完整圈所有的蚂蚁又回到初始状态，再考虑剩下的0.6。假设对于每一整圈，$x$只蚂蚁顺时针，$y$只蚂蚁逆时针，每圈相遇2次，那么相遇次数一共有$2xy$次相遇。这个根据均值不等式，显然对于N只蚂蚁，最大值为$2*(N/2)*(N-N/2)$。所以整圈最多有$2*(N/2)*(N-N/2)*10^5$。

接下来考虑剩下的0.6，由于初始位置是不同整数，所以只有位置相差1的蚂蚁才有可能相遇。这时候的相遇次数就是初始位置中最多选出多少个相差1的数对。

最终结果则是相加得到相遇次数再乘2，因为每次相遇两个蚂蚁会被计数。

## 代码

    #include <bits/stdc++.h>

    using namespace std;


    // Complete the solve function below.
    int solve(vector<int> V) {
        int N = V.size();
        int ans = 200000 * (N / 2) * (N - N / 2);
        vector<int> hash(1000, 0);
        for(int num:V) hash[num]++;
        for(int i=0;i<999;i++)
        {
            int minm = min(hash[i], hash[i + 1]);
            ans += minm;
            hash[i + 1] -= minm;
        }
        return ans * 2;

    }

    int main()
    {
        int N;
        cin>>N;
        vector<int> V(N, 0);
        for(int i=0;i<N;i++)
        {
            cin>>V[i];
        }
        cout<<solve(V);
        return 0;
    }


今天的整理就到这里啦~