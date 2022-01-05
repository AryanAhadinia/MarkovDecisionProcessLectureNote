# Introduction to Markov Decision Process

## Abstract

## Table of Contents

## Introduction


In nature, learning by trial and error is the most common way of learning. learning by trial and error is called Reinforcement Learning (RL) in computer literature. Markov Decision Process (MDP) is a foundational element of formulating reinforcement learning mathematically. In a typical Reinforcement Learning  problem, there is a learner and a decision maker called agent. The surrounding which agent interacts with is called environment. The environment provides rewards and a new state based on the actions of the agent. All these could be modeled in a single MDP. The environment is modeled with states, the 


Transition model is used to show thwie s So, in reinforcement learning, we do not teach an agent how it should do something but presents it with rewards whether positive or negative based on its actions. So the root question is how we formulate any problem in RL mathematically. This is where the Markov Decision Process (MDP) comes in.

## Markov Decision Process

Markov Decision Process is based on Markov chain. A Markov chain is a mathematical system that experiences transitions from one state to another according to certain probabilistic rules. The chain holds the following independence assumption.

$$ P(S_{t+1}|S_t, ..., S_0)=P(S_{t+1}|S_t) $$

$S_t$ represents the state at time $t$. Intuitively, $S_t$ conveys all of the information about the history that can affect the future states so the future is conditionally independent of the past, given the present.

### States

States are the feature representation of the data obtained from the environment. Thus, any input from the agent’s sensors can play an important role in state formation. The $ S $ state set is a set of different states, represented as $ s $ which shows the status of the envrironment.   Each MDP consists of some states, which some of them are stopping state or so called terminal state. Terminal state is a state in which no action could be taken. When agent enters a stopping state, sum of rewards, return, can be computed.

### Actions

Actions are set of things an agent is allowed to do in the given environment. The set of actions is usually showed with $ A $.

### Transition Model

At each state, the agent decides which action to perform. The resulting state (s') depends on both the current state (s) and the action performed by the agent (a). The transition model T(s, a, s’) gives probability P(s’|s, a), that is, the probability of landing up in the new  state s’ given that the agent takes an action, a, in given state, s.

Environments can be devided to two types according to their transition models.
- Determined environment: In a determined environment, if a certain action (a) is taken, the resulting state is the expected state (s') with probability 1.
- Stochastic environment: In a stochastic environment, if the same action (a) is taken, with a certain probability e.g. 0.8 the resulting state  will be the expected state and there is 0.2 probability that the resulting state is not the expected state. Here, for the s state and the a action transition model, T(s’, a, s) = P(s’| s, a) = 0.8.

### Rewards

The reward of the state quantifies the usefulness of taking a specific action and entering a state.These rewards incorporate the action costs in addition to any prizes or penalties that may be given. Negative rewards are called punishments. The general form of the reward function is shown as $ R(s, a, s') $. But in some MDPs the reward function is independent from the resulting state or both resulting state and action. In those models reward function is shown with $R(s, a) $ and $ R(s) $ respectively. 

For a particular environment, the domain knowledge plays an important role in the assignment of rewards for different states as minor changes in the reward do matter for finding the optimal solution to an MDP problem.
Sum of the rewards is called utility or return. 

### Formalization

By combining the concepts which were explained above the complete formulation for Markov Decision Process is acheived as below.

- A set of possible states $S$.
-	A set of possible actions $ A$.
-	A transition function $T(s, a, s’)$ 
    -  Probability that taking action $a$ in state $s$ leads to $s'$, i.e., $P(s’| s, a) $
- Also called the model or the dynamic.
- A reward function $R(s, a, s’) $
    - Sometimes reward only depends on the resulting state. So $R(s, a, s’)$ can be replaced by $R(s’)$ or $R(s', a)$
- A start state 
- Maybe a terminal state


## Policy

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

Due to previous discussions, now objective is to find policy that maximize expected discounted utility.
$$ max_\pi E \Bigg[ \sum_{i=0}^\infty \gamma^ir_i \Bigg] $$

Consider $V^*(s)$ as expected utility starting from state $s$ and act according to $\pi^*$, the optimal policy.

$Q^*(s, a)$ is expected utility starting from state $s$ then perform action $a$ and after that act according to $\pi^*$.

By considering all forward steps and choosing the step which maximize utility, $V^*$ can be formulated as
$$ V^*(s) = max_a Q^*(s, a) $$
and then by calculating expectation on earned utility by marginalizing on all possible next states which can be succeeded after action $a$ in state $s$, $Q^*$ will be written as
$$ Q^*(s, a) = \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V^*(s') \big]$$

Since $V^*$ and $Q^*$ are jointly recursive, It is possible to replace $Q^*$ in $V^*$.
$$ V^*(s) = max_a \sum_{s'}T(s, a, s')\big[R(s, a, s') + \gamma V^*(s') \big] $$

Equation above is called as *bellman equation*.

by solving bellman equation for all states, optimal policy will be obtained.

## Time Limited Values

## Conclusion

## References







<br><br><br><br><br><br><br><br>






### Discounting
Consider gaining reward $r_i$ in time step $t_i$. In discounting, $\sum \gamma^t_i r_i$ is considered instead of $\sum r_i$ as utility function such that $0\lt \gamma \lt 1$. $\gamma=1$ is just equivalent to simple summation. Apart from what we have said so far, this method has other advantages, which we will mention briefly below.

#### Infinite Utilities

#### Stationary Preference

