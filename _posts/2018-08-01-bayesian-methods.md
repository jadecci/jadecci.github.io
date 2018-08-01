---
layout: default
title:  "Bayesian Methods for Machine Learning"
date:   2018-08-01 16:53:00 +0800
categories: notes
---

# Bayesian Methods for Machine Learning
## 1. Introduction to Bayesian methods

### 1.1. Think Bayesian & statistics review
Principles:
1. use prior knowledge
2. choose what explains observations the most
3. avoid making extra assumptions

Independent events: $P(X,Y)=P(X)P(Y)$ \\
Conditional probability: $P(X|Y)=\frac{P(X,Y)}{P(Y)}$ \\
Or, chain rule: $P(X,Y)=P(X|Y)P(Y)$ \\
Marginal probability: $P(X)=\int p(X,Y) \mathop{dY}$ \\
==Bayes theorem: $P(\theta|X)=\frac{P(X|\theta)P(\theta)}{P(X)}$ => $Posterior = \frac{Likelihood \times Prior}{Evidence}$==

### 1.2. Bayesian approach to statistics
Frequentist: 
- $\theta$ is fixed, $X$ is random
- Maximum likelihood $\hat{\theta} =argmaxP(X|\theta)$

Bayesian:
- $\theta$ is random, $X$ is fixed
-  training: Posterior $P(\theta|X)=\frac{P(X|\theta)P(\theta)}{P(X)}$ 
-  prediction: 
$$
\begin{aligned}
P(y_{test}|X_{test}, X_{train}, y_{train}) &= \int P(y_{test}, \theta | X_{test}, X_{train}, y_{train}) \mathop{d\theta} \quad \text{(marginal)}\\
& =  \int P(y_{test}| \theta, X_{test}, X_{train}, y_{train}) P(\theta | X_{test}, X_{train}, y_{train}) \mathop{d\theta} \quad \text{(chains rule)}\\
& =\int P(y_{test}|X_{test}, \theta)P(\theta|X_{train}, y_{train}) \mathop{d\theta}
\end{aligned}
$$
- $P(\theta)$ also leads to regularisation
- online learning: $P_i(\theta)=P(\theta|x_i)=\frac{P(x_i|\theta)P_{i-1}(\theta)}{P(x_i)}$

### 1.3. How to define a model
Bayesian network (graph) 
- nodes : random variables
- edges: direct impact
- joint probability: $P(X_1, ..., X_n) = \prod_i P(X_i|Pa(X_i))$ where $Pa(X_i)$ means parents of $X_i$

Naive Bayes classifier: $P(c, f_1, ..., f_n) = P(c)\prod_i P(f_i|x)$ => plate notation
![plate notation](https://wiki.ubc.ca/images/thumb/e/ed/FpLDA1.jpg/550px-FpLDA1.jpg =300x120)

### 1.4. Linear regression
Least squares: $L(\omega) = \sum_i (\omega^Tx_i - y_i)^2 = \| \omega^Tx_i - y\|^2$
