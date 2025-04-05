#reinforcement_learning

![[_attachments/Pasted image 20250405091633.png]]
# Fundamental tools
 
## [[Chapter-1-Basic-Concept]]

- Concepts:
	- state
	- action
	- reward
	- return
	- episode
	- policy
- Grid world example
- Markov Decision Process——MDP

> [!warning] Attention
> Contents in [[Chapter-1-Basic-Concept]] are all fundamental concepts, which will be used **widely** and **frequently**

## [[Chapter-2-Bellman-Equation]]

- **One concept: state value** $$v_{\pi}(s) = \mathbb{E}[G_t | S_t = s]$$ State Value is the **mean**( $\mathbb{E}$ ) of **Return**( $G_t$ ) in some**State**( $t$ )

- **One tool: Bellman Equation** $$v_{\pi} = r_{\pi} + \gamma P_{\pi}v_{\pi}$$ Bellman Equation describes the **relationship** between **State** and **State Value**(get `State Value` from `State` by Bellman Equation to judge the performance of Policy $\pi$)

- **Policy Evaluation**
	- widely used later

## [[Chapter-3-Bellman-Optimality-Equation]]

> A special Bellman Equation---Bellman Optimality Equation

- Two concepts:
	- **Optimal Policy** $\pi^*$ : the policy which can get the greatest state value
	- **Optimal State Value** 
- One tool:**Bellman Optimality Equation**: $$v = \max_{\pi}(r_{\pi} + \gamma P_{\pi}v) = f(v)$$ 
	- Fixed_point theorem
		- Fundamental problems:  the Optimal State Value fundamentally exists
			- The Optimal Policy may not be only one while the Optimal State Value must be one
			- The Optimal Policy may be either **deterministic** (确定性的) or **stochastic** (随机性的)
		- An algorithm solving the equation --- Value Iteration (VI)
- **Optimality** 
	- widely used later

# Algorithms and Methods
## [[Chapter-4-Value-Iteration-and-Policy-Iteration]]

> First algorithms for optimal policies

- Three algorithms:
	1. **Value Iteration** (VI): calculate **one** step
	2. **Policy Iteration** (PI): calculate **infinite** steps
	3. **Truncated policy Iteration**: **cut off one step** in the middle
- Characteristic
	- **Policy update** and **Value update**
		- widely used later
	- **Need the environment model**

## [[Chapter-5-Monte-Carlo-Learning]]
> Model free learning

- Learn: **mean estimation with sampling data** $$\mathbb{E}[X] \approx \bar x = \frac{1}{n} \sum_{i = 1}^{n}x_i$$
- Algorithms:
	1. MC Basic
	2. MC Exploring Starts
	3. MC $\epsilon -\text{greedy}$ 

## [[Chapter-6-Stochastic-Approximation]]
- from **non-incremental** (非增量式) to **incremental** (增量式)
- Mean estimation
	- non-incremental: **sample and get mean estimation** (采样后取平均)
	- incremental: update the initial estimation when sampling new data (有初步估计，随着样本的采集来更新估计)
- Algorithms:
	- Robbins-Monro(RM) algorithm
	- Stochastic gradient decent(SGD) --- a special RM algorithm
	- SGD, Batch gradient decent(BGD), Mini batch gradient decent(MBGD)
- **incremental manner and SGD**
	- widely used later

## [[Chapter-7-Temporal-Difference-Learning]]

> Classic RL algorithms

- Algorithms:
	1. TD learning of **state values**
	2. Sarsa --- TD learning of **action values**
	3. Q-learning --- TD learning of **optimal action values** --- `off-policy`
		- `on-policy` vs `off-policy`
			- on-policy:
			- off-policy:

## [[Chapter-8-Value-Function-Approximation]]

> from `table representation` to `function representation` 

- Algorithms
	1. State value estimation with value function approximation (VFA) $$\min_{w}J(w) = \mathbb{E}[v_{\pi}(S) - \hat v (S, w)]$$
	2. Sarsa with VFA
	3. Q-learning with VFA
	4. Deep Q-learning
- Neural networks come into RL

## [[Chapter-9-Policy-Gradient-Methods]]

> from value-based to policy-based

- Contents
	1. Metrics to define optimal policies: $$J(\theta) = \bar v_{\pi} , \;\bar r_{\pi}$$
	2. Policy gradient: $$\nabla J(\theta) = \mathbb{E}[\nabla_{\theta} \ln{\pi}(A|S, \theta)q_{\pi}(S, A)]$$
	3. Gradient-ascent algorithm (REINFORCE): $$\theta_{t+1} = \theta_{t} + \alpha \nabla_{\pi} \ln{\pi(a_t|s_t, \theta_t)q_{t}(s_t, a_t)}$$

## [[Chapter-10-Actor-Critic-Methods]]

> value-based (Actor)+ policy-based (Critic)

$$\theta_{t+1} = \theta_{t} + \alpha \nabla_{\pi} \ln{\pi(a_t|s_t, \theta_t)\textcolor{orange}{q_{t}(s_t, a_t)}}$$
This formula is used to **update $\theta$ **

- Algorithms:
	1. The simplest actor-critic (QAC)
	2. Advantage actor-critic (A2C) : import a **baseline** to **reduce the variance** of the estimation
	3. Off-policy actor-critic
		- Importance Sampling: Transform on-policy actor-critic into off-policy actor-critic
	4. Deterministic actor-critic (DPG) and 1.-3. are Stochastic (stochastic action)

