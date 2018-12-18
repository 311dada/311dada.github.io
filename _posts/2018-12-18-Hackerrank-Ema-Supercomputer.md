---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Ema's Supercomputer       # 标题 
subtitle:   暴力大法
date:       2018-12-18           # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/two-pluses/problem'> 看题目戳我 </a>



## 题解思路
刚读题觉得好烦的题目，再一看数据范围，直接暴力。首先遍历两个加号的中心点位置，确定之后遍历每个加号大小，满足条件计数比较。

## 代码

    #include <bits/stdc++.h>

    using namespace std;



    // Complete the twoPluses function below.
    int twoPluses(vector<string> grid) {
        int m,n;
        m=grid.size();
        n=grid[0].length();
        int maxm=0;
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                for(int k=0;k<m;k++)
                {
                    for(int l=0;l<n;l++)
                    {
                        vector<int> tmp(n,0);
                        vector<vector<int>> mark(m,tmp);
                        for(int first=0;i-first>=0&&i+first<m;first++)
                        {
                            if(j-first<0||j+first>=n) break;
                            if(grid[i-first][j]!='G'||grid[i+first][j]!='G'||grid[i][j-first]!='G'||grid[i][j+first]!='G') break;
                            mark[i-first][j]=1;
                            mark[i+first][j]=1;
                            mark[i][j-first]=1;
                            mark[i][j+first]=1;
                            int first_area=1+4*first;
                            for(int second=0;k-second>=0&&k+second<m;second++)
                            {
                                if(l-second<0||l+second>=n) break;
                                if(grid[k-second][l]!='G'||grid[k+second][l]!='G'||grid[k][l-second]!='G'||grid[k][l+second]!='G') break;
                                if(mark[k-second][l]||mark[k+second][l]||mark[k][l-second]||mark[k][l+second]) break;
                                int second_area=1+4*second;
                                maxm = max(maxm,first_area*second_area);
                            }
                        }
                    }
                }
            }
        }
        return maxm;
    }

    int main()
    {
     
        int n,m;
        cin>>n>>m;
        vector<string> grid(n);

        for (int i = 0; i < n; i++) {
            string grid_item;
            cin>>grid_item;
            grid[i] = grid_item;
        }

        int result = twoPluses(grid);

        cout<<result;

        return 0;
    }


干就完事了！