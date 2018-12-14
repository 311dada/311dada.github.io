---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Points on a Rectangle         # 标题 
subtitle:   
date:       2018-12-11             # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/points-on-rectangle/problem'> 看题目戳我 </a>


## 题解思路
由于要判断的矩形是平行于坐标轴的，所以我们可以先根据这些点确定出这个矩形，然后判断剩余点是否在这个矩形上。

## 代码
    
    #include <bits/stdc++.h>

    using namespace std;

    // Complete the solve function below.
    string solve(vector<vector<int>> coordinates) {
        int maxmx=-100000,minmx=100000,maxmy=-100000,minmy=100000;
        for(auto it:coordinates)
        {
            maxmx = max(maxmx,it[0]);
            minmx = min(minmx,it[0]);
            maxmy = max(maxmy,it[1]);
            minmy = min(minmy,it[1]);
        }
        for(auto it:coordinates)
        {
            if(it[0]!=maxmx && it[0]!=minmx && it[1]!=minmy && it[1]!=maxmy) return "NO";
        }
        return "YES";
    }

    int main()
    {
        

        int q;
        cin >> q;

        for (int q_itr = 0; q_itr < q; q_itr++) {
            int n;
            cin >> n;
            vector<vector<int>> coordinates(n);
            for (int i = 0; i < n; i++) {
                coordinates[i].resize(2);

                for (int j = 0; j < 2; j++) {
                    cin >> coordinates[i][j];
                }
            }

            string result = solve(coordinates);

            cout << result << "\n";
        }


        return 0;
    }

    