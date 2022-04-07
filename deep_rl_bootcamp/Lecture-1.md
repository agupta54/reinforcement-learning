# Markov Decision Process

Agent: Gets to chose an action at time $t$, $a_t$

As a consequence the environment changes. The environment is the world around the agent.

Environment : After action state at $t+1$ is $s_{t+1}$ and reward $r_{t+1}$

**RL Algorithms landscape**: Policy Optimization and Dynamic Programming 

An MDP is defined by: 

* Set of states $S$
* Set of actions $A$
* Transition function $P(s'|s, a)$
* Reward function $R(s, a, s')$
* Start state $s_0$
* Discount factor $\gamma$
* Horizon $H$

**Goal**: $max_\pi E[\sum_{t=0}^H \gamma^t R(S_t, A_t, S_{t+1}) | \pi]$

Maximize expected sum of rewards under a policy $\pi$. Policy $\pi$ is a prescription which tells for each state what action you want to take. It could be a distribution over actions. But it can be a deterministic policy as well. 

***Optimal Control*** is given an MDP$(S,A,P,R,\gamma,H)$ find the optimal policy $\gamma^*$. This can be solved by exact methods by *value* iteration or *policy* iteration. 

## Optimal Value Function $V^*$

$$
V^*(s) = max_\pi E[\sum_{t=0}^H \gamma^t R(s_t, a_t, s_{t+1}) | \pi, s_0=s]
$$

= sum of discounted rewards when starting from state $s$ and acting optimally

## Value Iteration 

$V_0^*(s)$ = optimal value of state $s$ when $H=0$

Nothing can happen as there is no horizon left. $V_0^* = 0$,  $\forall s$

$V_1^*(s)$ = optimal value of state $s$ when $H=1$

$V_1^*(s) = max_a \sum_{s'} P(s'|s, a) (R(s, a, s') + \gamma V_0^*(s'))$

$V_2^*(s)$ = optimal value of state $s$ when $H=2$

$V_2^*(s) = max_a \sum_{s'} P(s'|s, a) (R(s, a, s') + \gamma V_1^*(s'))$

Similarly, 

$V_k^*(s)$ = optimal value for state s when $H=k$
$$
V_k^* = max_a \sum_{s'} P(s'|s, a)(R(s,a,s') + \gamma V_{k-1}^*(s'))
$$

## Value Iteration Convergence 

**Theorem**: Value iteration converges. At convergence, we have found the optimal value function $V^*$ for the discounted infinite horizon problem, which satisfies the Bellman equations. 
$$
\forall S \in S : V^*(s) = max_a \sum_{s'} P(s'|s, a)[R(s, a, s') + \gamma V^*(s')]
$$
Value iteration is a way to solve this equation in an efficient way. 

* Now we know how to act for infinite horizon with discounted rewards! 
  * Run value till convergence
  * This produces $V^*$, which in turn tells us how to act, namely following: 

$$
\pi^*(s) = arg max_a \sum_{s'} P(s'|s, a)[R(s, a, s') + \gamma V^*(s')]
$$

* The infinite horizon optimal policy is stationary. 

## Convergence: Intuition 

* $V^*(s)$ = expected sum of rewards accumulated starting from state $s$, acting optimally for $\infty$ steps. 

* $V^*_H(s)$ = expected sum of rewards accumulated starting from state $s$, acting optimally for $H$ steps.

* Additional reward collected over time steps $H+1$, $H+2$
  $$
  \gamma^{H+1}R(s_{H+1}) + \gamma^{H+2}R(s_{H+2}) + ... \leq \gamma^{H+1}R_{max} + \gamma^{H+2}R_{max} + ... = \dfrac{\gamma^{H+1}}{1-\gamma} R_{max}
  $$

## Convergence and Contractions 

* Define the max-norm: $\norm{U} = max_s \abs{U(s)}$
* **Theorem**: For any two approximations $U$ and $V$: 

$$
\norm{U_{i+1} - V_{i+1}} \leq \norm{U_i - V_i}
$$

i.e., any distinct approximations must get closer to each other.

## Q Values 

$Q^*(s, a)$ = expected utility starting in $s$, taking action $a$, and thereafter acting optimally

*Bellman Equation*: 
$$
Q^*(s,a) = \sum_{s'} P(s'|s, a)(R(s, a, s') + \gamma max_{a'}Q^*(s',a'))
$$
*Q-Value Iteration*
$$
Q^*_{k+1}(s, a) \leftarrow \sum_{s'} P(s'|s, a)(R(s, a, s') + \gamma max_{a'}Q^*_{k}(s',a'))
$$
