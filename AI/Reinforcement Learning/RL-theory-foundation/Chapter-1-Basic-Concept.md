# A grid world example

This book will use a grid world example since they are intuitive for illustrating new concepts and algorithms

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

> Attention!
> 1. Different states can have different action spaces
> 2. the most general case: $\textcolor{orange}{\mathcal{A}(s_i) = \mathcal{A} = {a_1, \dots, a_n} \text{ for all } i}$ 

### State transition
- **What is *state transition*?** When **taking an action**, the agent may **move from one state to another**.
- **How to express *state transition*?**   $s_1$ $\xrightarrow{a_2}$ $s_2$
- 
