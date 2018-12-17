---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Absolute Permutation         # 标题 
subtitle:   直接构造解
date:       2018-12-17           # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/absolute-permutation/problem'> 看题目戳我 </a>

## 注意事项
<b>下标是从1开始的</b>

## 题解思路
最先肯定是要举几个例子试一试咯。首先$k$是0的时候显然就是自然的序列。当$k>0$的时候，我们考虑在第$i$个位置上能放置什么数字。当$i\leq k$时，我们只能放$i+k$。所以有以下对应序列:
<p>
$$ 1,2,...,k$$
$$1+k,2+k,...,k+k$$
</p>
上面是下标序列，下面是对应的值。下面考虑第$k+1$位置，能放$1$和$2k+1$。但是我们反向考虑，$1$这个数字只能放到$k+1$位置。这样反向考虑，当数字$num\leq k$时，只能放到$num+k$位置。所以有:
<p>
$$1,2,...,k,k+1,k+2,...,2k$$
$$1+k,2+k,...,2k,1,2,...,k$$
</p>
所以满足条件的序列一定要满足上述块序列的组成。所以$n$必须是$k$的偶数倍。并且我们直接构造出了解，为保证字典序最小，只需要从小到大的连接块即可。

## 代码

    #include <bits/stdc++.h>

    using namespace std;


    // Complete the absolutePermutation function below.
    vector<int> absolutePermutation(int n, int k) {
        
        vector<int> res;
        if(k==0)
        {
          for(int i=1;i<=n;i++) res.push_back(i);
          return res;  
        }
        if(n%k!=0 || (n/k)%2!=0)
        {
            res.push_back(-1);
            return res;
        }
        int bias=0;
        for(int i=0;i<n/(2*k);i++)
        {
            for(int j=1;j<=k;j++) res.push_back(bias+k+j);
            for(int j=1;j<=k;j++) res.push_back(bias+j);
            bias += 2*k;
        }
        return res;
    }

    int main()
    {


        int t;
        cin >> t;

        for (int t_itr = 0; t_itr < t; t_itr++) {

            int n,k;
            cin>>n>>k;

            vector<int> result = absolutePermutation(n, k);

            for (int i = 0; i < result.size(); i++) {
                cout << result[i]<<' ';
            }
            cout<<endl;

        }


        return 0;
    }


下章见咯~