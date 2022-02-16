# Reinforcement Learning

## Introduction

Study of behaviour of subjects in some environment and optimize its behaviour.

## Markov Decision Process

Components involved:

* Decision Maker (Agent)

* Interactions occur sequentially over time.

* At each time step agent gets some representation of the environment state.

* Action taken by agent

* Environment moves to another state. 

* Agent gets a reward.

In an MDP we have a set of states **S**, a set of actions **A**, and a set of rewards **R**. We will assume that each of these sets has a finite number of elements.

At each time step t = 0, 1, 2, ..., the agent receives some representation of the environment's state $S_t \in \textbf{S}$. Based on this state, the agent selects an action $A_t \in \textbf{A}$. This gives us the state action pair ($S_t, A_t). $f$ is an arbitrary function that maps state-action pairs to rewards. At each time $t$, we have $  f(S_t, A_t) = R_{t+1} $.