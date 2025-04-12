## A grid world example

This book will use a grid world example since they are intuitive for illustrating new concepts and algorithms

![[Pasted image 20250408123821.png | Grid World Example]]
In grid world example: 
- yellow walls are ***forbidden*** that is not accessible or obtain a punishment for entry.
- white walls are ***accessible***.
- light blue wall is a ***target cell*** that the agent would like to reach.
# basic concepts

### State and Action
#### State
- **What is *state*?** State describes the agent's **status with respect to the environment**.
- **How to express *state*?** State is denoted as $s$. 
	- In grid world example, states are denoted as $s_1, s_2, \dots, s_9$
- **What is *state space*?** *State space* (the set of all states) is denoted as $\mathcal{S}$. In grid world example, state space is denoted as $\mathcal{S} = {s_1, \dots, s_9}$
#### Action
- **What is *action*?** Action describes the agent's action for one state.
- **How to express *action*?** Action is denoted as $a$. In grid world example, actions are denoted as $a_1, a_2, \dots, a_9$
- **What is *action space*?** Action space (the set of all actions for one state) is denoted as $\mathcal{A}$. In grid world example, action space is denoted as $\mathcal{A} = {a_1, \dots, a_9}$

> $\textcolor{red}{Attention!}$
> 1. Different states can have different action spaces
> 2. the most general case: $\textcolor{orange}{\mathcal{A}(s_i) = \mathcal{A} = {a_1, \dots, a_n} \text{ for all } i}$ 

### State transition
- **What is *state transition*?** When **taking an action**, the agent may **move from one state to another**.
- **How to express *state transition*?**   $s_1$ $\xrightarrow{a_2}$ $s_2$
	- The agent will **be bounced back** when **it attempts to go beyond the boundary,** for example, $s_1$ $\xrightarrow{a_1}$ $s_1$ 
	- The agent will **be bounced back when forbidden are not accessible** (for example, $s_5$ $\xrightarrow{a_2}$ $s_5$) or **get through when the forbidden are accessible** (for example, $s_5$  $\xrightarrow{a_2}$ $s_6$)
	- **Which scenario should we consider?** Depend on the physical environment.

#### *state transition process*
- **What is *state transition process*?** state transition process is **defined for each state and its associated actions** 

The following table is **a tabular representation of the *state transition process***.

|       |  $a_1 \text{ (upward)}$   | $a_2 \text{ (rightward)}$ | $a_3 \text{ (downward)}$  | $a_4 \text{ (leftward)}$  |   $a_5 \text{ (still)}$   |
| :---: | :-----------------------: | :-----------------------: | :-----------------------: | :-----------------------: | :-----------------------: |
| $s_1$ | $\textcolor{orange}{s_1}$ | $\textcolor{orange}{s_2}$ | $\textcolor{orange}{s_4}$ | $\textcolor{orange}{s_1}$ | $\textcolor{orange}{s_1}$ |
| $s_2$ | $\textcolor{orange}{s_2}$ | $\textcolor{orange}{s_3}$ | $\textcolor{orange}{s_5}$ | $\textcolor{orange}{s_1}$ | $\textcolor{orange}{s_2}$ |
| $s_3$ | $\textcolor{orange}{s_3}$ | $\textcolor{orange}{s_3}$ | $\textcolor{orange}{s_6}$ | $\textcolor{orange}{s_2}$ | $\textcolor{orange}{s_3}$ |
| $s_4$ | $\textcolor{orange}{s_1}$ | $\textcolor{orange}{s_5}$ | $\textcolor{orange}{s_7}$ | $\textcolor{orange}{s_4}$ | $\textcolor{orange}{s_4}$ |
| $s_5$ | $\textcolor{orange}{s_2}$ | $\textcolor{orange}{s_6}$ | $\textcolor{orange}{s_8}$ | $\textcolor{orange}{s_4}$ | $\textcolor{orange}{s_5}$ |
| $s_6$ | $\textcolor{orange}{s_3}$ | $\textcolor{orange}{s_6}$ | $\textcolor{orange}{s_9}$ | $\textcolor{orange}{s_5}$ | $\textcolor{orange}{s_6}$ |
| $s_7$ | $\textcolor{orange}{s_4}$ | $\textcolor{orange}{s_8}$ | $\textcolor{orange}{s_7}$ | $\textcolor{orange}{s_7}$ | $\textcolor{orange}{s_7}$ |
| $s_8$ | $\textcolor{orange}{s_5}$ | $\textcolor{orange}{s_9}$ | $\textcolor{orange}{s_8}$ | $\textcolor{orange}{s_7}$ | $\textcolor{orange}{s_7}$ |
| $s_9$ | $\textcolor{orange}{s_6}$ | $\textcolor{orange}{s_9}$ | $\textcolor{orange}{s_9}$ | $\textcolor{orange}{s_8}$ | $\textcolor{orange}{s_9}$ |

- **How to express *state transition process*?** 
	1. *tabular representation* above ---***Deterministic* state transitions only**
	2. $\textcolor{red}{\star}$ ***conditional probabilities*** ---**Both *deterministic* and *stochastic*** *state transitions*, denoted as $\textcolor{orange}{p(s'| s, a)}$
		- For example, for $s_1$ and $s_2$, the conditional probability distribution is 
			- $p(s_1|s_1,a_2)=0$
			- $p(s_2|s_1,a_2)=1$
			- $p(s_3|s_1,a_2)=0$
			- $p(s_4|s_1,a_2)=0$
			- $p(s_5|s_1,a_2)=0$
		- These indicate that, when take $a_2$ at $s_1$, **the probability of the agent moving to $s_2$ is $1$**, and the probabilities of the agent moving to other states are $0$

---
### Policy
- **What is *policy*?** *policy* tells the agent **which *actions* to take** at **every *state***. 
	- Following a *policy*, the agent can **generate a *trajectory* starting from an initial state**
- **How to express *policy*?** 
	- arrows in the grid world map
	- $\textcolor{red}{\star}$ ***conditional probabilities***: denoted as $\textcolor{orange}{\pi(a|s)}$
		- ***Deterministic policy***: **Only one policy** can be taken when taking actions at state $s_1$
			- For example, the policy for state $s_1$ is
				- $\pi(a_1|s_1)=0$
				- $\pi(a_2|s_1)=1$
				- $\pi(a_3|s_1)=0$
				- $\pi(a_4|s_1)=0$
				- $\pi(a_5|s_1)=0$
			- ![[Pasted image 20250408142536.png]]
			- These indicate that the probability of taking action $a_2$ at state $s_1$ is $1$, and the probabilities of taking other actions are $0$
		- ***Stochastic policy***: **Multiple policies** can be taken when taking actions at state $s_1$
			- For example, the policy for state $s_1$ is
				- $\pi(a_1|s_1) = 0$
				- $\pi(a_2|s_1) = 0.5$
				- $\pi(a_3|s_1) = 0.5$
				- $\pi(a_4|s_1) = 0$
				- $\pi(a_5|s_1) = 0$
			- ![[Pasted image 20250408142611.png]]
		- tabular conditional probabilities

|       | $a_1 \text{(upward)}$ | $a_2 \text{(rightward)}$ | $a_3 \text{(downward)}$ | $a_4 \text{(leftward)}$ | $a_5 \text{(still)}$ |
| :---: | :-------------------: | :----------------------: | :---------------------: | :---------------------: | :------------------: |
| $s_1$ |          $0$          |          $0.5$           |          $0.5$          |           $0$           |         $0$          |
| $s_2$ |          $0$          |           $0$            |           $1$           |           $0$           |         $0$          |
| $s_3$ |          $0$          |           $0$            |           $0$           |           $1$           |         $0$          |
| $s_4$ |          $0$          |           $1$            |           $0$           |           $0$           |         $0$          |
| $s_5$ |          $0$          |           $0$            |           $1$           |           $0$           |         $0$          |
| $s_6$ |          $0$          |           $0$            |           $1$           |           $0$           |         $0$          |
| $s_7$ |          $0$          |           $1$            |           $0$           |           $0$           |         $0$          |
| $s_8$ |          $0$          |           $1$            |           $0$           |           $0$           |         $0$          |
| $s_9$ |          $0$          |           $0$            |           $0$           |           $0$           |         $1$          |

---
### Reward
- **What is *reward*?** Feedback from environment after the agent executes an action at a state
- **How to express *reward*?** a function of the state $s$ and action $a$, which is denoted as $\textcolor{orange}{r(s,a)}$
	- Its value can be **positive** or **negative** real number or $0$. Different rewards have different impacts on the policy that agent would eventually learn
		- *positive reward*: **Encourage the agent to take the corresponding action**
		- *negative reward*: **Discourage the agent from taking that action**
> In the grid world example, the rewards are designed as follows:
>> If the agent attempts to exit the boundary $\rightarrow$ $r_{boundary}=-1$
>> If the agent attempts to enter a forbidden cell $\rightarrow$ $r_{forbidden} = -1$
>> If the agent reaches the *target state* $\rightarrow$ $r_{target}=1$
>> Otherwise, the agent obtains a reward of $r_{other} = 0$
>
>Some special conditions:
>> After reaching target state $s_9$, **the *reward process* does not have to terminate**
>>> For example:
>>> If agent takes action $a_5$ at $s_9$ $\rightarrow$ the next state is again $s_9$ && the reward plus 1 ($r_{target} +=1$)
>>> If agent takes action $a_3$ or $a_2$ $\rightarrow$ the next state is also $s_9$ while the reward subtract 1 $(r_{boundary} -=1$)

#### reward process
- **How to express *reward process*?** 
	1. tabular representation ---*Deterministic reward* only

|       | $a_1 \text{(upward)}$ | $a_2 \text{(rightward)}$ | $a_3 \text{(downward)}$ | $a_4 \text{(leftward)}$ | $a_5 \text{(still)}$ |
| :---: | :-------------------: | :----------------------: | :---------------------: | :---------------------: | :------------------: |
| $s_1$ |    $r_{boundary}$     |           $0$            |           $0$           |     $r_{boundary}$      |         $0$          |
| $s_2$ |    $r_{boundary}$     |           $0$            |           $0$           |           $0$           |         $0$          |
| $s_3$ |    $r_{boundary}$     |      $r_{boundary}$      |     $r_{forbidden}$     |           $0$           |         $0$          |
| $s_4$ |          $0$          |           $0$            |     $r_{forbidden}$     |     $r_{boundary}$      |         $0$          |
| $s_5$ |          $0$          |     $r_{forbidden}$      |           $0$           |           $0$           |         $0$          |
| $s_6$ |          $0$          |      $r_{boundary}$      |      $r_{target}$       |           $0$           |   $r_{forbidden}$    |
| $s_7$ |          $0$          |           $0$            |     $r_{boundary}$      |     $r_{boundary}$      |   $r_{forbidden}$    |
| $s_8$ |          $0$          |       $r_{target}$       |     $r_{boundary}$      |     $r_{forbidden}$     |         $0$          |
| $s_9$ |    $r_{forbidden}$    |      $r_{boundary}$      |     $r_{boundary}$      |           $0$           |     $r_{target}$     |
- 
	2. conditional probabilities ---Both *deterministic* and *stochastic*, **denoted as** $\textcolor{orange}{p(r|s,a)}$
		- For example, for state $s_1$, we have
			- $p(r=-1|s_1,a_1)=1$
			- $p(r\neq -1 |s_1, a_1)=0$

---
### Trajectories, returns, and episodes

#### *trajectory*
- **What is *trajectory*?** A *state-action-reward* chain
	- For example, $s_1$ $\xrightarrow[r=0]{a_2}$ $s_2$ $\xrightarrow[r=0]{a_3}$ $s_5$ $\xrightarrow[r=0]{a_3}$ $s_8$ $\xrightarrow[r=0]{a_2}$ $s_9$ 

#### *return*
- **What is *return*?** also called ***total rewards*** or ***cumulative rewards*** **the sum of all the rewards collected along the *trajectory***
	- For example, $\text{return} = 0 + 0 + 0 + 1 = 1$
- **What does *return* consist of?** an *immediate reward* and *future rewards*
	- *immediate reward*: the reward obtained after taking an action **at** the initial state
	- *future rewards*: the total rewards obtained after **leaving** the initial state
- ***return* can be defined for infinitely long *trajectories***
	- For example, we can design a policy so that the agent stays still after reaching *target cell* $s_9$. 
		- The trajectory: $s_1$ $\xrightarrow[r=0]{a_2}$ $s_2$ $\xrightarrow[r=0]{a_3}$ $s_5$ $\xrightarrow[r=0]{a_3}$ $s_8$ $\xrightarrow[r=0]{a_2}$ $s_9$ $\xrightarrow[r=0]{a_5}$ $s_9$ $\xrightarrow[r=0]{a_5}$ $s_9 \dots$ 
		- The direct sum of the rewards along the trajectory: $\text{return}=0+0+0+1+1+1+\dots+\infty$
		- The *discounted return* (with *discount rate* in order to make return converge) along the trajectory: $\text{discounted return}=0+\gamma 0+\gamma^2 0 + \gamma^3 1 + \gamma^4 1 + \gamma^5 1 + \dots \text{ ,  } \gamma \in(0,1)$
			- *discounted return* can be calculated as $\text{discounted return} = \gamma^3(1+\gamma + \gamma^2 + \dots) = \gamma^3\frac{1}{1-\gamma}$

##### The reason for using *discount rate* $\gamma$
1. $\gamma$ removes the stop criterion and **allows for infinitely long trajectories**
2. $\gamma$ can be used to **adjust the emphasis placed on near- or far-future rewards**
	- If $\gamma$ is close to $0$ $\xrightarrow{then}$ **near future** rewards have **more emphasis** and **the policy would be *short-sighted***
	- If $\gamma$ is close to $1$ $\xrightarrow{then}$ **far future** rewards have **more emphasis** and **the policy would be *far-sighted***

#### *episode*
- **What is *episode*?** When interacting with the environment by following a policy, the agent may **stop at some *terminal states***. The result trajectory is called an *episode* or a *trial*
	- If the environment or policy is *stochastic* $\rightarrow$ we obtain **different episodes** when **starting from the same state**
	- If the environment or policy is *deterministic* $\rightarrow$ we always obtain **same episodes when starting form the same state**
- **An episode is usually assumed to be a finite trajectory**

##### *episodic tasks*
- **What is *episodic tasks*?** Tasks with episodes

###### *continuing tasks*
- **What is *continuing tasks*?** Some tasks without terminal states

###### convert *episodic tasks* into *continuing tasks*
After reaching the terminal state in an *episodic task*, the agent can continue taking actions in two ways:
1. ***Absorbing states**: Treat the *terminal state* as a special state. We can design its *action space* or *state transition* so that the agent **stays in this state forever**---*absorbing states*
	- For example: for the *target state* $s_9$, we can specify $\mathcal{A}(s_9) = {a_5}$ or set $\mathcal{A}(s_9) = {a_1, \dots, a_5} \text{ with } p(s_9|s_9,a_i) = 1 \text{ for all } i=1,\dots,5$
2. $\textcolor{red}{\star}$ **Normal states**: Treat the *terminal state* as a normal state. We can simply **set its action space to the same as the other states, and the agent leave and come back again**. Every time $s_9$ is reached, **the agent will eventually learn to stay at $s_9$ forever to collect more rewards**. While, a discount rate must be used to calculate the discounted return to **avoid divergence**
---
### Markov Decision Process
> An MDP is a general framework for describing *stochastic dynamical systems*

#### key ingredients of an MDP
- Sets:
	- *state space*: the set of all states, denoted as $\mathcal{S}$
	- *action space*: the set of all actions, denoted as $\mathcal{A}(s)$, associated with each state $s \in \mathcal{S}$
	- *reward space*: the set of rewards, denoted as $\mathcal{R}(s,a)$, associated with state-action pair $(s,a)$
- Model:
	- *State transition probability*: In state $s$, when taking action $a$, the probability of transitioning to state $s'$ is $\textcolor{orange}{p(s'|s,a)}$. It holds $\sum_{s' \in S}p(s'|s,a) = 1$ for any $(s,a)$
	- *Reward probability*: In state $s$, when taking action $a$, the probability of obtaining reward $r$ is $\textcolor{orange}{p(r|s,a)}$. It holds $\sum_{r \in R(s,a)}p(r|s,a) = 1$ for any $(s,a)$
- Policy:
	- In state s, the probability of choosing action $a$ is $\textcolor{orange}{\pi(a|s)}$. It holds $\sum_{a \in \mathcal{A}(s)}\pi(a|s) = 1$
- Markov property: 
	- the *Markov property* refers to the memoryless property of a *stochastic process*.
	- $$\textcolor{orange}{p(s_{t+1}|s_t, a_t, s_{t-1}, a_{t-1},\dots,s_{0},a_{0})=p(s_{t+1}|s_t,a_t)}$$
	- $$\textcolor{orange}{p(r_{t+1}|s_t, a_t, s_{t-1}, a_{t-1},\dots,s_{0},a_{0})=p(r_{t+1}|s_t,a_t)}$$
		- $t$: represents the **current time step**.
		- $t+1$: represents the **next time step**.
		- $\textcolor{red}{\star}$ *Markov property* is important for deriving the fundamental Bellman equation of MDPs, as shown in the next chapter

##### stationary models and nonstationary models
- $\textcolor{red}{\star}$ stationary models: does not change over time.
- nonstationary models: may vary over time.
	- For example in the *grid world example*, if a forbidden area may pop up or disappear sometimes, the model is nonstationary

##### Markov processes(MPs)
- Relationship between MDPs and MPs: $\text{MDPs}$ ${\xrightarrow[\text{degenerates}]{\text{fixed policy}}}$ $\text{MPs}$
- $\textcolor{red}{\star}$ Markov chain: a discrete-time process and the number of states is **finite** or **countable**
![[截屏2025-04-08 17.36.25.png]]
 
***
### Summary
- *reinforcement learning* can be described as **an agent-environment interaction process**.
- The *agent* is a **decision-maker**
	- sense its state.
	- maintain policies.
	- execute actions.
- **Everything outside of the agent is regarded as the environment**. (In the grid world example, the agent and environment correspond to the robot and the grid world)
- After the agent decides to take an action, the actuator executes such a decision.
- Then, **the state of the agent would be changed** and **a reward can be obtained**
- By using interpreters, the agent can **interpret the new state and the reward.**
