# CS 188 - Project 3: Reinforcement Learning

## 简介

本项目旨在实现并应用强化学习中的两种核心算法：**价值迭代 (Value Iteration)** 和 **Q学习 (Q-Learning)**。通过在一个马尔可夫决策过程 (MDP) 环境中训练智能体 (Agent)，我们能够找到最优策略，使其在不确定的世界中做出最佳决策。

智能体将在三个不同的环境中进行测试：
1.  **Gridworld**: 一个经典的网格世界，用于验证和调试价值迭代算法。
2.  **Crawler**: 一个模拟的机器人，它需要学习如何向前移动。
3.  **Pacman**: 我们的老朋友吃豆人，它将利用Q学习来学习如何在躲避鬼魂的同时吃掉所有的豆子，而无需预先了解游戏规则。

本项目主要修改的文件是 `valueIterationAgents.py` 和 `qlearningAgents.py`。

---

## 安装与环境

本项目基于 Python 3.x 开发。开始之前，请确保你已经安装了所有必要的依赖。通常情况下，项目本身不依赖于外部库，可以直接运行。

-   **Python**: 3.6 或更高版本
-   **Tkinter**: 用于图形化界面展示。大多数Python发行版已自带。如果缺失，请根据你的操作系统进行安装（例如，在Ubuntu上使用 `sudo apt-get install python3-tk`）。

使用方法与指令
你可以通过命令行运行不同的模块来测试和展示你实现的算法。以下是本项目中常用的一些命令。

1. 价值迭代 (Value Iteration)
价值迭代算法在 valueIterationAgents.py 中实现。你可以使用 gridworld.py 来可视化智能体通过价值迭代计算出的策略。

运行默认的Gridworld
运行价值迭代智能体，默认进行100次迭代。

```bash

python gridworld.py -a value -i 100
```
-a value: 指定使用价值迭代智能体。

-i 100: 设置迭代次数为100。

你可以看到每个网格的状态价值以及最终学到的策略（以箭头形式表示）。

修改参数运行
可以修改迭代次数、噪声和折扣因子等参数来观察策略的变化。

改变迭代次数:

```Bash

python gridworld.py -a value -i 5
```
（只进行5次迭代，价值尚未完全收敛）

改变噪声 (Noise):

```Bash

python gridworld.py -a value -i 100 -n 0.0
```
（-n 0.0 表示没有噪声，行动结果是确定的）

改变生存奖励 (Living Reward):

```Bash

python gridworld.py -a value -i 100 -r -0.1
```
（-r -0.1 表示每走一步都有一个小的负奖励，鼓励智能体尽快到达终点）

2. Q学习 (Q-Learning)
Q学习算法在 qlearningAgents.py 中实现。我们主要在 Pacman 环境下测试该算法。

训练Pacman Q-Learning智能体
在 smallGrid 地图上训练 PacmanQAgent 2000轮游戏，并观看最后10轮的表现。

```Bash

python pacman.py -p PacmanQAgent -x 2000 -n 2010 -l smallGrid
```
-p PacmanQAgent: 指定使用Q学习吃豆人智能体。

-x 2000: 设置训练轮次 (number of training episodes)。

-n 2010: 设置总共运行的游戏轮次。训练将在前2000轮进行，最后10轮将关闭学习（探索率epsilon为0），只展示学习到的策略。

-l smallGrid: 指定使用的地图布局。

训练近似Q学习智能体 (Approximate Q-Learning)
对于更复杂的地图（如 mediumGrid），状态空间太大，无法使用传统的Q表。此时需要使用近似Q学习，通过特征来估计Q值。

```Bash

python pacman.py -p ApproximateQAgent -a extractor=SimpleExtractor -x 50 -n 60 -l mediumClassic
```
-p ApproximateQAgent: 指定使用近似Q学习智能体。

-a extractor=SimpleExtractor: 指定用于提取状态特征的函数。SimpleExtractor 是一个预先提供的基本特征提取器。

3. Crawler 机器人
你也可以在 crawler.py 上测试你的Q学习算法，训练一个两足机器人学习如何行走。

```Bash

python crawler.py
```
这个脚本会打开一个图形界面，并自动开始训练过程。你可以实时观察到机器人学习行走的过程以及奖励的变化。
