---
layout: post
title: "5 DQN Methods"
subtitle: ''
author: "Tianming Qiu"
header-style: text
mathjax: true
tags:
  - RL
  - DQN
---
## Key papers
1. [Playing Atari with Deep Reinforcement Learning](https://www.cs.toronto.edu/~vmnih/docs/dqn.pdf), Mnih et al, 2013. Algorithm: DQN.
2. [Deep Recurrent Q-Learning for Partially Observable MDPs](https://arxiv.org/pdf/1507.06527.pdf), Hausknecht and Stone, 2015. Algorithm: Deep Recurrent Q-Learning.
3. Dueling Network Architectures for Deep Reinforcement Learning, Wang et al, 2015. Algorithm: Dueling DQN.
4. [Deep Reinforcement Learning with Double Q-learning](https://arxiv.org/pdf/1509.06461.pdf), Hasselt et al 2015. Algorithm: Double DQN.
5. Prioritized Experience Replay, Schaul et al, 2015. Algorithm: Prioritized Experience Replay (PER).
6. Rainbow: Combining Improvements in Deep Reinforcement Learning, Hessel et al, 2017. Algorithm: Rainbow DQN.

## Double DQN
区别在于，传统DQN在target net中，放入是s_next，挑选最大q值，而double是把s_next放入eval_net，得到最大Q值的动作索引，去索引target net的Q值

## PER
- [Note](http://www.meltycriss.com/2018/03/18/paper-prioritized-experience-replay/)
- [SumTree](https://www.cnblogs.com/pinard/p/9797695.html)
- [PrefixSum Implementation](https://github.com/TianmingQiu/DeepRL-Tutorials)
- [Sample along probability-prefix Sum](https://www.geeksforgeeks.org/random-number-generator-in-arbitrary-probability-distribution-fashion/)
- [Explain on Sumtree k segments](https://jaromiru.com/2016/11/07/lets-make-a-dqn-double-learning-and-prioritized-experience-replay/)
- [MorvanZhou](https://morvanzhou.github.io/tutorials/machine-learning/reinforcement-learning/4-6-prioritized-replay/)
- [A same question as yours](https://stats.stackexchange.com/questions/362036/prioritized-experience-replay-per)



