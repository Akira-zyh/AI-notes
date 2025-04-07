# Optimal policy

> The **state value** can be used to evaluate if a policy is good or not

when $\pi_1$ is better than $\pi_2$ :
$$v_{\pi_1}(s) \ge v_{\pi_2} \; \text{ for all } s \in S$$
So, a policy $\pi^*$ is optimal if $v_{\pi^*}(s) \ge v_{\pi}(s)$ **for all $s$ **and for **any other policy $\pi$**

While this definition leads to many questions:
- Does the optimal policy *exist*?
- Is the optimal policy *unique*?
- Is the optimal policy *stochastic* or *deterministic*?
- How to *obtain* the optimal policy

$\textcolor{red}{\star}$ **Bellman Optimality Equation**(BOE) can answer questions all above.

---
# Bellman Optimality Equation(BOE)

1. BOE  **element-wise form**
$$\textcolor{orange}{v(s) = \max_{\pi} \sum_{a} \pi(a|s) \bigg(\sum_r p(r|s, a)r + \gamma\sum_{s'}p(s'|s,a)v(s')\bigg), \forall s \in S}$$
simplify : $$\textcolor{orange}{v(s) = \max_{\pi} \sum_a \pi(a|s) q(s|a), \forall s \in S}$$
Remarks:
- $\gamma$, $p(r|s, a)$ and $p(s'|s, a)$ are known.
- $v(s)$ and $v(s')$ are unknown and to be calculated.
- $\pi(s)$ is unknown in BOE and to be calculated.($\pi(s)$ is given in BE)

---
2. BOE **matrix-vector form**
$$\textcolor{orange}{v = \max_{\pi}(r_{\pi} + \gamma P_{\pi}v)}$$
where the element corresponding to $s$ or $s'$ are
$$[r_{\pi}]_s \triangleq \sum_a \pi(a|s) \sum_r p(r|s,a)r$$
$$[P_{\pi}]_{s,s'} = p(s'|s) \triangleq \sum_a \pi(a|s) \sum_{s'}p(s'|s,a)$$
> BOE describes **the optimal policy and optimal state value** in an elegant way

Some questions to answer: 
- Algorithm: how to solve this question?
- Existence: does this equation have solutions?
- Uniqueness: is the solution to this equation unique?
- Optimality: how is it related to optimal policy?

---

### Some Tricks of BOE
Maximization on the right-hand side of BOE is about **two** unknown variables, which seems to be difficult to solve

$\star$ Example
Suppose $q_1,q_2,q_3 \in \mathbb{R}$ are given and $q3 \geq q1, q2$. Find $c_1^*, c_2^*, c_3^*$ solving 
$$\max_{c_1, c_2, c_3} c_1q_1 + c_2q_2 + c_3q_3$$where $c_1 + c_2 + c_3 = 1$  and $c_1, c_2, c_3 \geq 0$. **Then**, the optimal solution is $c_3^* = 1$ and $c_1^* = c_2^* = 0$. Because, for any $c_1, c_2, c_3$:
$$q_3 = (c_1 + c_2 + c_3)q_3 = c_1q_3 + c_2q_3 + c_3q_3 \ge c_1q_1 + c_2q_2 + c_3q_3$$
---

### Solution of BOE
Inspired by the above example, **considering that**  $\sum_a \pi(a|s) = 1$, we have
$$\max_{\pi} \sum_a \pi(a|s) q(s,a) = \max_{a \in \mathcal{A}(s)} q(s,a)$$
where the optimality is achieved when 
$$\pi(a|s) = \begin{cases} 
&1 ,&a = a^* \\
&0 ,& a \neq a^*
\end{cases}
\;\; \text{ where } a^* = \arg\max_{a} q(s,a)
$$

