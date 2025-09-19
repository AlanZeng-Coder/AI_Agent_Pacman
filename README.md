CS 188 Project 3: Reinforcement Learning
Project Overview
This project explores the core concepts of Markov Decision Processes (MDPs) and Reinforcement Learning (RL) by implementing RL algorithms for agents in two environments: Gridworld and Pac-Man.

The primary goal is to build agents that can learn optimal policies in unknown environments through interaction. The project implements and analyzes two fundamental reinforcement learning algorithms:

Value Iteration: A model-based dynamic programming algorithm used to find the optimal value function and policy for a known MDP.

Q-Learning: A model-free temporal-difference learning algorithm that learns the optimal action-value function (Q-function) directly from experience, without needing a model of the environment.

These algorithms are first tested in a simple Gridworld and then applied to control a simulated Crawler robot and, finally, the Pac-Man agent.

File Structure
valueIterationAgents.py: Contains the implementation of the Value Iteration agent, which solves for the optimal policy assuming the MDP's dynamics (transitions and rewards) are known.

qlearningAgents.py: Implements the Q-Learning agent and the Approximate Q-Learning agent. These agents learn from the outcomes of their actions ((state, action, nextState, reward) tuples) to operate in environments where the transition and reward models are unknown.

analysis.py: Includes written answers to analytical questions about the behavior of the agents and the impact of various parameters (e.g., discount factor, learning rate, exploration rate).

gridworld.py: The Gridworld environment simulator.

featureExtractors.py: Provides functions to extract features from a game state, used by the Approximate Q-Learning agent.

How to Run the Code
Gridworld Examples
Q1: Value Iteration
Run value iteration for 100 iterations on the default Gridworld.

Bash

python gridworld.py -a value -i 100
-a value: Use the ValueIterationAgent.

-i 100: Perform 100 iterations of value updates.

Q4 & Q5: Q-Learning
Train a Q-Learning agent for 50 episodes in the Gridworld.

Bash

python gridworld.py -a q -k 50 -n 0 -g 0.9 -e 0.1
-a q: Use the QLearningAgent.

-k 50: Run for 50 training episodes.

-g 0.9: Set the discount factor γ to 0.9.

-e 0.1: Set the exploration rate ε to 0.1.

Crawler Robot
Run the crawler robot simulation to have it learn to walk.

Bash

python crawler.py
Pac-Man
Q6: Q-Learning Pac-Man
Train a PacmanQAgent. Training is done with the display turned off by default for speed.

Bash

# Train the agent on the smallGrid for 2000 episodes
python pacman.py -p PacmanQAgent -x 2000 -n 2010 -l smallGrid

# Watch the trained agent play 10 games
python pacman.py -p PacmanQAgent -n 10 -l smallGrid -a numTraining=2000
-p PacmanQAgent: Use the Q-Learning Pac-Man agent.

-x 2000: Specify 2000 training episodes.

-l smallGrid: Use the smallGrid layout.

Q7: Approximate Q-Learning Pac-Man
For larger, more complex layouts, standard Q-Learning is infeasible due to the massive state space. Here, we use an agent that learns weights for features instead of Q-values for states.

Bash

# Train the approximate agent on the mediumClassic layout for 50 episodes
python pacman.py -p ApproximateQAgent -a extractor=SimpleExtractor -x 50 -n 60 -l mediumClassic

# Watch the trained approximate agent play
python pacman.py -p ApproximateQAgent -a extractor=SimpleExtractor -n 10 -l mediumClassic
-p ApproximateQAgent: Use the feature-based Q-Learning agent.

-a extractor=SimpleExtractor: Specify the feature extractor to use.

Summary of Implemented Concepts
Q1: Value Iteration
In valueIterationAgents.py, the agent computes the optimal value V*(s) for each state by iteratively applying the Bellman update until convergence. The optimal policy π*(s) is then extracted from these values.

Q2 & Q3: Analysis
These questions, answered in analysis.py, explore the theoretical aspects of MDPs. By adjusting parameters like the living reward and discount factor, we can design policies that exhibit specific behaviors (e.g., preferring a distant but larger reward while avoiding risks), demonstrating a deep understanding of the trade-offs in reinforcement learning.

Q4 & Q5: Q-Learning
The QLearningAgent was implemented in qlearningAgents.py. This agent learns a Q-table from scratch through trial and error. Key methods implemented include update, computeActionFromQValues, and getAction. An epsilon-greedy strategy is used to balance exploration (trying random actions) and exploitation (choosing the best-known action).

Q6: Pac-Man Q-Agent
The standard Q-Learning algorithm was applied to Pac-Man. The state representation was carefully defined to make learning feasible. After thousands of training games, the agent learns an effective policy for eating dots and avoiding ghosts without any prior knowledge of the game's rules.

Q7: Approximate Q-Learning
To handle the enormous state space of larger Pac-Man maps, we implemented an ApproximateQAgent. This agent uses a linear function to approximate the Q-value:
Q(s, a) = w₁f₁(s, a) + w₂f₂(s, a) + ...
Instead of learning a table of Q-values, the agent learns a weight vector w for a set of features (e.g., distance to the nearest food, presence of nearby ghosts). This allows the agent to generalize its knowledge to states it has never seen before, enabling it to perform well on complex layouts.
