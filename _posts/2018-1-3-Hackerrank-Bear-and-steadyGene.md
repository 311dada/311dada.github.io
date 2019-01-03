---
layout:     post                    # 使用的布局（不需要改）
title:      HackerRank Problem Bear-and-steadyGene         # 标题 
subtitle:   滑动窗口
date:       2018-1-3         # 时间
author:     An automatic pencil                      # 作者
header-img:     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   HackerRank                      #标签
---

## 题目

<a href='https://www.hackerrank.com/challenges/bear-and-steady-gene/problem'> 看题目戳我 </a>



## 题解思路
这个题目初次看到很自然的就会先考虑到先统计一下每种字符的数目，然后比较一下每种字符的数目和$n/4$的关系。不难知道，我们显然是把数目比较多的字符变到$n/4$，对所有字符做完这一点显然就能达到目的。

考虑我们要操作的子串，两端记为$l$和$r$,如果这一段<b>对于每种字符都不低于多出$n/4$的那些数目</b>，我们就能把多的字符变少。而且需要注意一个性质，就是如果一个字符串不满足上面加黑的性质，那么他的字串也不满足。这个时候我们就能用滑动窗口法了。如果对于当前固定的$l$,选择当前$r$不满足加黑性质，那么我们增加$r$来扩充字符就好了。如果满足，记录一下结果。此时我们不必要再增加$r$，因为增加只会增大结果。此时我们需要改变增加$l$,但是$r$没必要退回，因为退回的话是个之前已经考察过的不满足加黑性质字符串的某个字串。这一点就是滑动窗口的应用本质。所以我们可以继续保持$r$对于当前更新的$l$继续上述操作。

## 代码

    #include <bits/stdc++.h>

    using namespace std;

    char ch[4]={'A','T','C','G'};

    bool judge(map<char,int> mp,map<char,int> left,map<char,int> right)
    {
        for(int i=0;i<4;i++)
        {
            if(right[ch[i]]-left[ch[i]]<mp[ch[i]]) return false;
        }
        return true;
    }
    int main()
    {
        int n;
        cin>>n;
        string s;
        cin>>s;
        map<char,int> left,right,mp;
        for(int i=0;i<4;i++)
        {
            left[ch[i]]=0;
            right[ch[i]]=0;
            mp[ch[i]]=0;
        }
        for(int i=0;i<n;i++)
        {
            mp[s[i]]++;
        }
        for(int i=0;i<4;i++)
        {
            mp[ch[i]]-=n/4;
        }
        int l=-1,r=-1,ans=n;
        while(r<n && l<=r)
        {
            
            if(judge(mp,left,right))
            {
                ans=min(ans,r-l);
                l++;
                left[s[l]]++;
            }
            else
            {
                r++;
                if(r>=n) break;
                right[s[r]]++;
                
                
                
            }
        }
        
        cout<<ans;
        return 0;
    }


可能初次接触滑动窗口不是很好理解，最好手动模拟一下操作~