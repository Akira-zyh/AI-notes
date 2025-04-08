# A grid world example

This book will use a grid world example since they are intuitive for illustrating new concepts and algorithms

![[Pasted image 20250408123821.png | Grid World Example]]
In grid world example: 
- yellow walls are ***forbidden*** that is not accessible or give punishment for entry.
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
	2. $\textcolor{red}{\star}$ ***conditional probabilities*** ---**Both *deterministic* and *stochastic*** *state transitions*
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
	- $\textcolor{red}{\star}$ ***conditional probabilities***: denoted as $\pi(a|s)$
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
- **How to express *reward*?** a function of the state $s$ and action $a$, which is denoted as $r(s,a)$
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
	2. conditional probabilities ---Both *deterministic* and *stochastic*
