# Introduction to Markov Decision Process

## Abstract

## Table of Contents

## Introduction

## Formalization

## Policy

## MDP Search Trees

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

In a typical Reinforcement Learning (RL) problem, there is a learner and a decision maker called agent and the surrounding with which it interacts is called environment. The environment, in return, provides rewards and a new state based on the actions of the agent. So, in reinforcement learning, we do not teach an agent how it should do something but presents it with rewards whether positive or negative based on its actions. So the root question is how we formulate any problem in RL mathematically. This is where the Markov Decision Process (MDP) comes in.
Markov Decision Process is based on Markov chain. A Markov chain is a special sort of belief network used to represent the sequence of states in a dynamic system. The belief network holds the following independence assumption.

$$ P(S_{t+1}|S_t, ..., S_0)=P(S_{t+1}|S_t) $$

$S_t$ represents the state at time $t$. Intuitively, $S_t$ conveys all of the information about the history that can affect the future states. At $S_t$, It can be seen that the future is conditionally independent of the past given the present. At each state, the agent decides which action to perform. The resulting state depends on both the previous state and the action performed by the agent. Each action has a reward which sum of these rewards is called return.




### Discounting
Consider gaining reward $r_i$ in time step $t_i$. In discounting, $\sum \gamma^t_i r_i$ is considered instead of $\sum r_i$ as utility function such that $0\lt \gamma \lt 1$. $\gamma=1$ is just equivalent to simple summation. Apart from what we have said so far, this method has other advantages, which we will mention briefly below.

#### Infinite Utilities

#### Stationary Preference

