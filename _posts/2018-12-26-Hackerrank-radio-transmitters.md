---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Radio-Transmitters         # 标题 
subtitle:   贪心法
date:       2018-12-26          # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/hackerland-radio-transmitters/problem'> 看题目戳我 </a>



## 题解思路
首先看个例子:

<div  align="center">    
    <img src="https://s3.amazonaws.com/hr-challenge-images/26945/1477492663-b1b6a9502e-k-nearest22.png" width = "75%" height = "100%" alt="图像无法显示" />
</div>

上图是题目中的一个例子，首先在数轴上标记出每个位置，然后从左到右先看2，如果在2放置，那么4会收到信号。再看4，如果在4放置，那么2，5，6都会收到信号。再看5，如果5放置，2就收不到信号了，所以为保证2能收到信号，显然在4放置更好。因为在4放置能保证左边覆盖掉的同时，右边尽可能大。然后后面的放置是一个道理。

实际做完这个操作，很自然的我们就采用这个贪心法。首先在数轴上写数字的过程其实就相当于先从小到大排个序，然后从左到右扫描。然后我们需要记录当前要放置的信号源要覆盖的最左边房子的位置和即将要放置信号源的当前最棒的位置。当扫描到的点不在当前放置信号源的覆盖范围内时，这时候我们需要新放置信号源，而且新信号源需要覆盖的最左边位置也要更新。当扫描到的点在当前放置信号源的覆盖范围内时，我们要看看信号源能不能放到当前新扫描的点来贪心，如果当前点和当前信号源覆盖的最左点距离不大于信号源辐射距离，我们就能把信号源放在新扫描点。否则，我们就什么都不做，继续判断后续点就可以啦。

## 代码

    #include <bits/stdc++.h>

    using namespace std;

    int main()
    {
        int n,k;
        cin>>n>>k;
        vector<int> location(n);
        for(int i=0;i<n;i++) cin>>location[i];
        sort(location.begin(),location.end());
        int pre=location[0],left=location[0],ans=1;
        for(int i=0;i<n;i++)
        {
            if(location[i]>pre+k)
            {
                ++ans;
                left=location[i];
                pre=location[i];
            }
            else if(location[i]-left<=k) pre = location[i];
        }
        cout<<ans;
        return 0;
    }

今天就到这里咯0.0