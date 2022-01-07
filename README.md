# Introduction to Markov Decision Process

## Abstract

## Table of Contents

## Introduction


In nature, learning by trial and error is the most common way of learning. learning by trial and error is called Reinforcement Learning (RL) in computer literature. Markov Decision Process (MDP) is a foundational element of formulating reinforcement learning mathematically. In a typical Reinforcement Learning  problem, there is a learner and a decision maker called agent. The surrounding which agent interacts with is called environment. The environment provides rewards and a new state based on the actions of the agent. All these could be modeled in a single MDP. The environment is modeled with states and agent's possible decisions are modeled by actions. Since In real problems unexpected events may happen, agent's actions may not lead to expected results. This is why MDP models are used. 
Transition model is used to show thwie s So, in reinforcement learning, we do not teach an agent how it should do something but presents it with rewards whether positive or negative based on its actions. So the root question is how we formulate any problem in RL mathematically. This is where the Markov Decision Process (MDP) comes in.

## Markov Decision Process

Markov Decision Process is based on Markov chain. A Markov chain is a mathematical system that experiences transitions from one state to another according to certain probabilistic rules. The chain holds the following independence assumption.

$$ P(S_{t+1}|S_t, ..., S_0)=P(S_{t+1}|S_t) $$

$S_t$ represents the state at time $t$ . Intuitively, $S_t$ retains all of the information about the history that can affect the future states so *the future is conditionally independent of the past, given the present*.

### States

A representation of the environment's features at a specific time is called state and shown by $s$. Thus, any input from the agent’s sensors can play an important role in state formation. The $S$ state set is a set of different states, represented as $s$ which shows the status of the envrironment.   Each MDP consists of some states, which some of them are stopping state or so called terminal state. Terminal state is a state in which no action could be taken. When agent enters a stopping state, sum of rewards, return, can be computed.

### Actions

Actions are set of operations an agent is allowed to do in the given environment. The set of actions is usually shown with $A$.

### Transition Model

At each state, the agent decides which action to perform. The resulting state ($s'$) depends on both the current state ($s$) and the action performed by the agent ($a$). The transition model $T(s, a, s’)$ gives probability $P(s’|s, a)$, that is, the probability of landing up in the new  state $s’$ given that the agent takes an action, $a$, in the given state, $s$.

Environments can be devided to two types according to their transition models.
- Determined environment: In a determined environment, if a certain action ($a$) is taken, the resulting state is the expected state ($s'$) with probability 1.
- Stochastic environment: In a stochastic environment, if the same action (a) is taken, with a certain probability ,e.g. $0.8$, the resulting state  will be the expected state and there is $0.2$ probability that the resulting state is not the expected state. Here, for the state $s$, the action $a$ and next state $s'$ the transition model is $T(s’, a, s) = P(s’| s, a) = 0.8$.

### Rewards

The reward function, quantifies the usefulness of taking a specific action and entering a specific state. These rewards incorporate the action costs in addition to any prizes or penalties that may be given. Negative rewards are called punishments. The general form of the reward function is shown as $R(s, a, s')$. But in some MDPs the reward function is independent from the resulting state or both resulting state and action. In those models reward function is shown with $R(s, a)$ and $R(s)$ respectively. 

For a particular environment, the domain knowledge plays an important role in the assignment of rewards for different states as minor changes in the reward do matter for finding the optimal solution to an MDP problem.
Sum of the rewards is called *utility* or *return*.

Usually the performance of the agent, which is also called *utility*, is measured by the sum of rewards on the visited path. But other utility fucntions are also possible. General form of utility is shown by $U_h[s_0,s_1, s_2, ..., s_N]$.  



### Formalization

By combining the concepts which were explained above the complete formulation for Markov Decision Process is acheived as below.

- A set of possible states $S$.
-	A set of possible actions $A$.
-	A transition function $T(s, a, s’)$ 
    -  Probability that taking action $a$ in state $s$ leads to $s'$, i.e., $P(s’| s, a)$
- Also called the model or the dynamic.
- A reward function $R(s, a, s’)$
    - Sometimes reward only depends on the resulting state. So $R(s, a, s’)$ can be replaced by $R(s’)$ or $R(s', a)$
- A start state 
- Maybe a terminal state


### Policy

The policy is a function that takes the state as an input and outputs the action to be taken. Policy $\pi : S \rightarrow A$ is a set of commands that the agent follows.

The policy which maximizes the expected utility among all the possible policies is called optimal policy and shown with $\pi^*$. 

Finding $\pi^*$ is usually refered to as solving the MDP. There are different algorithms which attempt to find $\pi^*$ such as value iteration and policy evaluation.


## MDP Search Trees

In expectimax tree the path which leads to the most reward is desired. MDP problems could be demostrated as a search tree. But there are two main differences.
- In MDP Rewards are assigned to edges rather than nodes.
- In MDP utiliy is the sum of rewards gained in the path to the terminal state. But in expectimax utility is the the value assigned to the terminal state. 

## Utilities of Sequences

It's easy to choose between sequence of [1, 2, 2] and [2, 3, 4]. Obviously more return as well as more reward is gained in each step. But choosing between [1, 0, 0] and [0, 0, 1] is not that easy. This motivates us to consider the time which the reward is being received. In most cases, it's preferred to gain the rewards as soon as possible.

### Discounting

#### Infinite Utilities

#### Stationary Preference

## Bellman Equation

Due to previous discussions, now objective is to find policy that maximizes expected discounted utility.
$$ max_\pi E \Bigg[ \sum_{i=0}^\infty \gamma^ir_i \Bigg] $$

Consider $V^*(s)$ as expected utility starting from state $s$ and act according to $\pi^*$, the optimal policy.

$Q^*(s, a)$ is the expected utility starting from state $s$ then performing action $a$ and after that acting according to $\pi^*$.

By considering all forward steps and choosing the step which maximizes the utility, $V^*$ can be formulated as
$$ V^*(s) = max_a Q^*(s, a) . $$
Then by calculating expectation on earned utility by marginalizing on all possible next states which can be succeeded after action $a$ in state $s$, $Q^*$ will be written as
$$ Q^*(s, a) = \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V^*(s') \big].$$

Since $V^*$ and $Q^*$ are jointly recursive, It is possible to replace $Q^*$ with $V^*$.
$$ V^*(s) = max_a \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V^*(s') \big] $$

Equation above is called as *bellman equation*.

By solving bellman equation for all states, optimal policy will be obtained.

## Time Limited Values

Solving bellman equation via tree has two major problems:

1. There are repeating sub problems, so there are a lots of overheads on the system.
2. The depth of the tree could be infinite.

An approach to solve this problem is to try solving the problem in $k$ steps which converge to final answer instead of one-shot solving.

Instead of $V^*(s)$, Consider $V_k(s)$ which is the expected utility starting from state $s$ and acting according to $\pi^*$ with consideration that the process will be terminated after $k$ steps. The idea is that with the growth of $k$, $V_k$ will converge to $V^*$ so an approximate solution to the equations system can be optained.

Equations below are the limited form of what was discussed about $V^*$ and $Q^*$ above.
$$ V_{k+1}(s) = max_a Q_k(s, a) $$
$$ Q_k(s, a) = \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V_k(s') \big]$$

So $V_{k+1}$ can be calculated by
$$ V_{k+1}(s) = max_a \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V_k(s') \big] .$$

For each state $s$, $V_{k+1}(s)$ will be calculated by iteration over all states and all actions, which has time complexity $O(|S||A|)$. So the total time complexity for each iteration will  be $O(|S|^2|A|)$.

## Conclusion

In conclution Markov Decision Process is an appropriate tool to represent Reinforcement Learning problems. In order to represent a problem using MDP, states, actions, transition model and rewards should be determined properly. Afterwards finding the optimal policy, i.e. the one with the most utility, is desired. In order to find the optimal utility, bellman equation should be solved. Algorithms such as value iteration and policy iteration attempt to solve the bellman equation feasibly. In the end take into consideration that in real world Reinforcement Learning problems, the transiton model and reward function are not known and must be learned.


## References

- https://towardsdatascience.com/real-world-applications-of-markov-decision-process-mdp-a39685546026
- https://web.mit.edu/6.246/www/notes/L3-notes.pdf
- https://hub.packtpub.com/reinforcement-learning-mdp-markov-decision-process-tutorial/
- http://artint.info/html/ArtInt_160.html#stationary-Markov-Chain
- https://towardsdatascience.com/introduction-to-reinforcement-learning-markov-decision-process-44c533ebf8da
- https://www.geeksforgeeks.org/markov-decision-process/






<br><br><br><br><br><br><br><br>






### Discounting
Consider gaining reward $r_i$ in time step $t_i$. In discounting, $\sum \gamma^t_i r_i$ is considered instead of $\sum r_i$ as utility function such that $0\lt \gamma \lt 1$. $\gamma=1$ is just equivalent to simple summation. Apart from what we have said so far, this method has other advantages, which we will mention briefly below.

#### Infinite Utilities

#### Stationary Preference

Decision making problems may be of two types. Some may be *finite horizon* and some *infinite horizon*. Finite horizon means that there is a fixed time N after which nothing matters. In other words what happens after the fixed time is not analysed. To be mathematically shown, $U_h([s_0, s_1,...,s_{N+k}]) = U_h([s_0, s_1,..., s_N ])$
for all $k > 0$ . In finite horizon problems, the optimal action in a given state could change over time. For example when there is little time left, the agent should take risk to gain reward before the deadline is reached. Because of this change in optimal action in a given state over time, the optimal policy for a finite horizon is nonstationary. However, with no fixed time limit, there is no reason to behave differently in the same state at different times. Hence, the optimal policy depends only on the current state, and the optimal policy is stationary. Note that infinite horizon does not necessarily mean that all state sequences are infinite, it just means that there is no fixed deadline.

In infinite horizon a natural preference-independence is held. The agent’s preferences between state sequences are stationary. Stationarity for preferences means

$[s, s_0, s_1, s_2,  ... ] > [s, s_0', s_1', s_2',  ... ] \iff [s_0, s_1, s_2,  ... ] > [s_0', s_1', s_2',  ... ].$

This means that if a sequence is prefered to another, it is also prefered after one state is passed. Explaning is simple words, this means that if one future is prefered  to another starting tomorrow, then it is still prefered if it were to start today instead. 
