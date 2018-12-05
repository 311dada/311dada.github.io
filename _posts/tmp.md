---
layout:     post                    # 使用的布局（不需要改）
title:      强化学习（一）         # 标题 
subtitle:   初识强化学习及概念理解
date:       2018-12-5             # 时间
author:     An automatic pencil                      # 作者
header-img: img/RL1.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:   Reinforcement learning                        #标签
---

## 初步了解强化学习

初识强化学习的人一般都会见到下面这张图：

<div  align="center">    
    <img src="https://spinningup.openai.com/en/latest/_images/rl_diagram_transparent_bg.png" width = "50%" height = "50%" alt="图像无法显示" />
</div>

强化学习的基本设想是一个智能体(agent)与环境(environment)交互，当智能体采取一个动作(action)后，环境的状态(state)会发生一个改变，并且会对智能体反馈一个奖励(reward)来评价这个动作。

举个例子：

<div  align="center">    
    <img src="https://s1.ax1x.com/2018/12/05/FlFcfe.png" width = "20%" height = "20%" alt="图像无法显示" />
</div>

相信这款类似的游戏大家都玩过，智能体就是小鸟，不做任何操作小鸟会向前和下降，环境就是小鸟所处的游戏环境，小鸟向上和不向上就是它的动作，假如它没有死亡，奖励设置为1，死亡奖励设置为-1000。直观上理解，强化学习通过小鸟一次又一次的尝试游戏，根据奖励更改自己的行为方式。

强化学习的基本假设：
<font color="#0000dd">所有的目标都是最大化智能体获得的累计奖励。</font><br /> 

## 强化学习概念理解及标注符号

<font color="#006666">动作</font>: $a$表示智能体采取的一个动作。

<font color="#006666">动作空间</font>: $A$表示智能体可以采取的所有的动作集合，有限集。

<font color="#006666">状态</font>: 状态有环境的状态和智能体的观测状态之分。环境的状态能表示所处环境的所有信息，而智能体的观测状态只包括智能体可以观测的信息。理论上我们需要的状态是环境状态，但是智能体获取的是观测状态，而环境的有些信息可能是无法观测的。这时候我们通过构建合适的描述可以让观测状态近似环境状态，所以实际操作过程中常用$s$（智能体观测状态）代表环境状态。

<font color="#006666">状态空间</font>: $S$表示所有可能状态的集合，有限集。

<font color="#006666">轨迹</font>: $<s_0,a_0,s_1,a_1,...>$是一个智能体与环境相对于时间的交互序列，称它为一个轨迹(episode)，记为$\tau$。对于上面的小鸟游戏来讲，一局游戏便会产生一个轨迹。

<font color="#006666">策略</font>: 智能体会只根据当前状态，不考虑历史状态选取一个动作，那么如何选取这个动作被称为策略(policy)

## 马尔可夫性

## 马尔可夫过程

## 马尔可夫奖励过程

## 马尔可夫决策过程

## 值函数

