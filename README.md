# Reinforcement Learning

## Introduction

This project implements and applies two core reinforcement learning algorithms: **Value Iteration** and **Q-Learning**. By training an agent in a Markov Decision Process (MDP) environment, we can find an optimal policy that allows the agent to make the best decisions in a world of uncertainty.

The agent is tested in three distinct environments:
1.  **Gridworld**: A classic grid-based world used to validate and debug the Value Iteration algorithm.
2.  **Crawler**: A simulated robot that must learn how to move forward.
3.  **Pacman**: Our old friend Pacman, who will use Q-Learning to learn how to eat all the dots while avoiding ghosts, without any prior knowledge of the game's rules.

The primary files modified for this project are `valueIterationAgents.py` and `qlearningAgents.py`.

---

## Setup and Environment

This project is developed in Python 3.x. Before you begin, please ensure you have all necessary dependencies installed. The project generally does not rely on external libraries and can be run directly.

-   **Python**: Version 3.6 or higher.
-   **Tkinter**: Used for the graphical user interface. Most Python distributions include it by default. If it is missing, please install it according to your operating system (e.g., on Ubuntu, use `sudo apt-get install python3-tk`).

### Getting the Project Files

First, obtain the project code by cloning the repository or downloading the zip file.

```bash
git clone <your-repository-link>
cd <repository-name>
```
Usage and Commands
You can run the different modules from the command line to test and demonstrate your implemented algorithms. Below are some of the common commands used in this project.

1. Value Iteration
The Value Iteration algorithm is implemented in valueIterationAgents.py. You can use gridworld.py to visualize the policy computed by the agent.

Running the Default Gridworld
Run the value iteration agent for 100 iterations by default.

```Bash

python gridworld.py -a value -i 100
```
-a value: Specifies the value iteration agent.

-i 100: Sets the number of iterations to 100.

You will see the value of each state in the grid and the final learned policy (represented by arrows).

Running with Modified Parameters
You can change parameters like the number of iterations, noise, and discount factor to observe how the policy changes.

Change iterations:

```Bash

python gridworld.py -a value -i 5
```
(With only 5 iterations, the values will not have fully converged.)

Change noise:

```Bash

python gridworld.py -a value -i 100 -n 0.0
```
(-n 0.0 means there is no noise, so actions are deterministic.)

Change living reward:

```Bash

python gridworld.py -a value -i 100 -r -0.1
```
(-r -0.1 applies a small negative reward for each step, encouraging the agent to reach the terminal state faster.)

2. Q-Learning
The Q-Learning algorithm is implemented in qlearningAgents.py. This algorithm is primarily tested in the Pacman environment.

Training the Pacman Q-Learning Agent
Train the PacmanQAgent on the smallGrid layout for 2000 games and watch the performance of the final 10 games.

```Bash

python pacman.py -p PacmanQAgent -x 2000 -n 2010 -l smallGrid
```
-p PacmanQAgent: Specifies the Q-Learning Pacman agent.

-x 2000: Sets the number of training episodes.

-n 2010: Sets the total number of games to run. Training occurs during the first 2000 episodes, and for the final 10, learning is turned off (epsilon = 0) to display the learned policy.

-l smallGrid: Specifies the map layout to use.

Training the Approximate Q-Learning Agent
For more complex layouts like mediumClassic, the state space is too large for a traditional Q-table. In this case, Approximate Q-Learning is required, which estimates Q-values using features.

```Bash

python pacman.py -p ApproximateQAgent -a extractor=SimpleExtractor -x 50 -n 60 -l mediumClassic
```
-p ApproximateQAgent: Specifies the Approximate Q-Learning agent.

-a extractor=SimpleExtractor: Specifies the function used to extract features from states. SimpleExtractor is a basic feature extractor provided in the project.

3. Crawler Robot
You can also test your Q-Learning algorithm on the crawler.py environment to train a two-legged robot to walk.

```Bash

python crawler.py
```
This script will open a graphical interface and automatically begin the training process. You can observe the robot learning to walk and the reward progression in real-time.

Running the Autograder
The project includes an autograder to check the correctness of your implementation.

Run All Tests
To run the complete test suite, execute the following command:

```Bash

python autograder.py
```
Run Tests for a Specific Question
If you only want to test a single question (e.g., q1), you can use the -q flag:

```Bash

python autograder.py -q q1
```
View Graphical Tests
Some test cases support graphical display to help with debugging.

```Bash

python autograder.py --graphics -q q4
```
This will run the test for question 4 with visualization.
