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



## Skip frames vs. frames stack
- In the DQN(2013), it illustrates a frame-skipping technique: 
> Following previous approaches to playing Atari games, we also use a simple frame-skipping technique[$^3$](https://www.jair.org/index.php/jair/article/view/10819). More precisely, the agent sees and selects actions on every $k^{th}$ frame instead of every frame, and its last action is repeated on skipped frames. Since running the emulator forward for one step requires much less computation than having the agent select an action, this technique allows the agent to play roughly $k$ times more games without significantly increasing the runtime. We use $k = 4$ for all games except Space Invaders where we noticed that using $k = 4$ makes the lasers invisible because of the period at which they blink. We used $k = 3$ to make the lasers visible and this change was the only difference in hyperparameter values between any of the games.

- While DeepMind DQN series use [ALE](https://www.jair.org/index.php/jair/article/view/10819) and we usually use [OpenAI Gym platform](https://gym.openai.com/envs/Breakout-v0/), there is a difference between these two that OpenAI Gym skips the frames randomly by uniformly samples $k$ from $\{2,3,4\}$ instead of fixes $k=4$. Hence, we use a modified OpenAI Gym called [deterministic version](https://github.com/openai/gym/blob/5cb12296274020db9bb6378ce54276b31e7002da/gym/envs/__init__.py#L352), which explains in this [blog](https://becominghuman.ai/lets-build-an-atari-ai-part-1-dqn-df57e8ff3b26?gi=a6144d070ba4).
- Actually Atari games were treated as POMDP:
> Since the agent only observes images of the current screen, the task is partially observed and many emulator states are perceptually aliased, i.e. it is impossible to fully understand the current situation from only the current screen $ x_t $. We therefore consider sequences of actions and observations, $s_t = x_1, a_1, x_2, ..., a_{t−1}, x_t $, and learn game strategies that depend upon these sequences.

- Both 13 DQN and 16 Double Q Learning stack last four frames to represent a state:
> *13 DQN*: For the experiments in this paper, the function $\phi$ from algorithm 1 applies this preprocessing to the last 4 frames of a history and stacks them to produce the input to the Q-function.

> *16 Double Q Learning*: The network takes the last four frames as input and outputs the action value of each action.