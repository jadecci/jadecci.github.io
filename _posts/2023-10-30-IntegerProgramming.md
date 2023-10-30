---
layout: default
title:  "Integer Programming"
date:   2023-10-30 17:06:00 +0100
categories: notes
tags: Computing
---

This set of notes includes formulation and solving techniques for integer programming, based on the MIT computing course. 

## 1. Formulation

In order to formulate an interger programming problem, we start by formulating the conditions in the problem just like in a linear problem, and then by adding constraints or modifying existing constraints to enforce the interger constraints on variables. A basic cost function may look like:

$$
z = \sum^{n}_{i=1} c_{i} x_{i} \text{,} \quad \text{subject to: } x_i \ge 0 \text{, } x_i \text{ integer for all $i$}
$$

Usually, an interger programming problem imposes logical constraints in a realistic situation, while limiting certain variables to be integers. For instance, a goods storage problem may constrain the total amount of goods that can be stored in a variable number of warehouses; reality demands that the number of warehouses has to be an integer. Assuming the integer variable is still $x$ in this case, we may add an additional constraint:

$$
\sum^{n}_{i=1} a_{i} x_{i} - By \le b \text{,} \quad y = 0 \text{ or } 1
$$

where the binary variable $y$ determines whether this constraint is enforced based on certain other conditions. For instance, only one constraint from two constraints is chosen to be in effect each time, the constraints would look like:

$$
\sum^{n}_{i=1} a_{i} x_{i} - B_1 y_1 \le b_1 \text{, } \sum^{n}_{i=1} a_{i} x_{i} - B_2 y_2 \le b_2 \\
y_1 + y_2 \le 1 \text{, } y_1 \text{, } y_2 = 0 \text{ or } 1
$$

The constraints can also be represented in terms of equalities, by making use of slack variables $s$:

$$
\sum^{n}_{i=1} a_{i} x_{i} - By - s = b \text{,} \quad y = 0 \text{ or } 1 \text{, } s \ge 0
$$

In some cases, the constraint cannot be represented by a scalar $b$ as it varies based on the value of $x$. This means that the constraint is a piecewise linear function of $x$. We can represent compute the constraint based on the piecewise segments:

$$
b = m_1 \delta_{1} + m_2 \delta_{2} + ... + m_k \delta_{k} \\
L_k \omega_j \le \delta_k \le L_k \omega_{k-1}
$$

where $L_k$ is the length of the segment $\delta_k$, $\omega$ is an integer varaible with $\omega_k = 1$ if $\delta_k$ is at its upper bound, and $\omega_k = 0$ otherwise.

## 2. Solving Techniques

### 2.1. Branch-and-Bound

This is a divide-and-conquer strategy, based on the knowledge that the objective or penalty of an equivalent linear formuation ($z^0$) will always be an upper bound on the optimal objective of the integer formulation. The integer objective would be $z^* = floor(z^0)$ with a solution set of $x^0_i$s.

Then, we branch out for each $x_i$ dividing the solution space into $x_i \le ceil( x^0_i )$ and $x_i \le floor(x^0_i)$. For instance, if the optimal solution for $x_1$ is $x^0_1 = 3.25$, the two subdivisions of the solution space would thus be $x_1 \le 4$ and $x_1 \ge 3$. In this way, the optimal solution is contained in boths subdivisions. Note that within each branch, we need to recompute $x^0_{i+1}$ adding the constraints used for the division,  which gives us the conditions for splitting further for $x_{i+1}$. Some subdivisons may be infeasible as they violate constraints in the base formuation.

After branching out for all $x_1$ to $x_n$, we should have between $1$ to $2^n$ subdivisons to consider. For each subdivision, we can recompute the set of $x^0$ and check if all $x_i$s are intergers. If they are not, then we continue to divide the subdivision until an interger solution is found or until the sub-sub-sub-...-subdivision become infeasible. In the case where more than one variables need to be solved, only integer variables would cause further dividing, as the non-integer ones are simply solved while solving the linear formulation each time.

At any point during the process, if an integer solution is found with an objective $\hat{z}$, then all subdivisions where the optimal objective of the linear function $z^*$ is worse than $\hat{z}$ can be discarded.

Quite obviously, the computational time of a branch-and-bound algorithm is dependant on which subdivision is investigated first. However, there is no universal method for picking the best subdivison to start with, as one cannot guess the optimal intergal objective based on the optimal linear objective. Several heuristic procedures have been in use, including starting with the subdivision with the largest optimal linear objective value, and ruling on a last-generated-first-analyzed absis.

#### 2.1.1. Implicit Enumeration

If all variables concerned are binary, a spcial branch-and-bound procedure called implicit enumeration can be used, which does not require solving an equivalent linear formuation. We simply branch out for each $x_i$ into $x_i = 0$ and $x_i = 1$. In order to avoid branching out at every level when $n$ is large, some subdivisions can be determined to be unworthwhile without being explored.

One approach is to prune some subdivisions based on the coefficient in the base formulation. For instance, for an $x_i$ where the coefficient $c_i$ is positive, the objective to maximise will always be better with $x_i = 1$ than $x_i = 0$. In this case, the subdivision of $x_i = 0$ only needs to be considered if the subdivision $x_i = 1$ is infeasible.

Another approach would be to compute the *infeasibility* of each subdivisions before exploring, and start with subdivisions with the lowest *infeasibility*. The value of *infeasibility* can be measured by the deviation from $b$ in each sub-subdivision, and totaled across all sub-sub-sub-...-subdivisions.

#### 2.1.2. Implementation

For Python users, the package `pybnb` provides an implementation of a parallel branch-and-bound engine ([readthedocs](https://pybnb.readthedocs.io/en/stable/index.html)).

### 2.2. Cutting Planes

The cutting-plane approach refines the linear function with additional constraints, which reduces the solution space, until only a single set of integer solution is left. In practice, the cutting-plane algorithm is generally considered inefficient, and the branch-and-bound procedures are preferred. Nevertheless, this algorithm provided basis and inspirations for more efficient algorithms later; understanding the working of this algorithm would therefore be beneficial.

To illustrate, consider the following integer problem:

$$
\begin{aligned}
z & = 7x_1 + 5x_2 \text{,} \\
\text{subject to: } & x_1 + x_2 + s_1 = 6, \\
& 2x_1 + 5x_2 + s_2 = 23 \\
& x_1,x_2, s_1, s_2 \ge 0 \text{ and integers}
\end{aligned}
$$

Combining the constraints allow us to represent $x_1$ and $x_2$ in terms of $s_1$ and $s_2$:

$$
\begin{aligned}
x_1 & = \frac{7}{3} - \frac{5}{3}s_1 + \frac{1}{3}s_2 \\
x_2 & = \frac{11}{3} + \frac{2}{3}s_1 - \frac{1}{3}s_2
\end{aligned}
$$

This then let us rewrite our cost function and the two constraints:

$$
\begin{aligned}
-z - 9s_1 - 34 & =  \frac{2}{3} - \frac{2}{3}s_1 - \frac{2}{3}s_2 \\
x_1 +  s_1 - s_2 - 2 & = \frac{1}{3} - \frac{2}{3}s_1 - \frac{2}{3}s_2 \\
5x_2 - 4s_1 + s_2 - 18 & = \frac{1}{3} - \frac{2}{3}s_1 - \frac{2}{3} s_2 \\
\end{aligned}
$$

For all three equations, we can see that their left-hand-sides are integers, while their right-hand-sides are less than $\frac{2}{3}$, $\frac{1}{3}$ and $\frac{1}{3}$ respectively. Since the two sides are equal for each equation, they thus have to be $0$ or negative integers. This means that we now have two additional constraints (as the last two are identical):

$$
\begin{aligned}
\frac{2}{3} - \frac{2}{3}s_1 - \frac{2}{3}s_2 - s_4 & = 0 \text{, } \quad s_4 \ge 0 \text{ and integer} \\
\frac{1}{3} - \frac{2}{3}s_1 - \frac{2}{3}s_2 - s_5 & = 0 \text{, } \quad s_5 \ge 0 \text{ and integer} \\
\end{aligned}
$$

These two additional constraints are called "cuts". By adding more and more cuts, we will close in on the optimal integer solution. In practice, the number of cuts required to get to the optimal integer solution tend to be large, causing the algorithm to be inefficient.
