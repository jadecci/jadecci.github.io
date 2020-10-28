---
layout: default
title:  "Distributions and Derivations"
description: "General Notes"
date:   2019-04-17 15:07:00 +0100
categories: notes
---

This set of notes include information and derivations for some statistical distributions, including gamma distribution and the t-distribution. 


This note includes information and derivations for some useful statistical distributions. Currently this includes gamma, beta, $\chi^2$ (incomplete) and t distributions.

## 1.  Gamma Distribution ($x \in [0,\infty)$)
Gamma function: $\Gamma(n) = \int^{\infty}_0 x^{n-1}e^{-x} \mathop{dx} = (n-1)!$

Proof by math induction:

$$
\Gamma(1) =  \int^{\infty}_0 e^{-x} \mathop{dx} = -e^{-x}\big|^{\infty}_0= 1 = 0!\\
\begin{aligned}
\Gamma(n+1) &= \int^{\infty}_0 x^n e^{-x} \mathop{dx} \\
& = -x^n e^{-x} \big|^{\infty}_0 + n\int^{\infty}_0 x^{n-1} e^{-x} \mathop{dx} \\
& = n\int^{\infty}_0 x^{n-1} e^{-x} \mathop{dx} \\
& = n\Gamma(n)
\end{aligned}
$$

Gamma distribution: 

$$
\Gamma(\gamma | a,b) = \frac{b^a}{\Gamma(a)} \gamma^{a-1} e^{-b\gamma}
$$

Expectation:

$$
\begin{aligned}
\mathbb{E}[\gamma] &= \int^{\infty}_0 \gamma \frac{b^a}{\Gamma(a)} \gamma^{a-1} e^{-b\gamma} \mathop{d\gamma}\\
& = \int^{\infty}_0 (\frac{a}{b}) \frac{b^{a+1}}{\Gamma(a+1)} \gamma^a e^{-b\gamma} \mathop{d\gamma} \\
& = \frac{a}{b} \int^{\infty}_0 \Gamma(a+1,b) \mathop{d\gamma} \\
& = \frac{a}{b} \quad \text{(integral of pdf is 1)}
\end{aligned}
$$

Mode:

$$
\begin{aligned}
\mathrm{Mode}[\gamma] &= \mathrm{arg\,max}_\gamma  \frac{b^a}{\Gamma(a)} \gamma^{a-1} e^{-b\gamma} \\
i.e. \quad & \frac{\partial}{\partial\gamma} \gamma^{a-1} e^{-b\gamma} = 0 \\
& (-b\gamma + a-1)\gamma^{a-2} e^{-b\gamma} = 0 \\
\therefore \mathrm{Mode}[\gamma] & = \frac{a-1}{b}
\end{aligned}
$$

Variance:

$$
\begin{aligned}
\mathrm{Var}[\gamma] &=  \int^{\infty}_0 \gamma^2 \frac{b^a}{\Gamma(a)} \gamma^{a-1} e^{-b\gamma} \mathop{d\gamma} - \mathbb{E}[\gamma]^2\\
& = \int^{\infty}_0 (\frac{a(a+1)}{b^2}) \frac{b^{a+2}}{\Gamma(a+2)} \gamma^{a+1} e^{-b\gamma} \mathop{d\gamma} - (\frac{a}{b})^2\\
& = \frac{a(a+1)}{b^2} - (\frac{a}{b})^2  \quad \text{(integral of pdf is 1)} \\
& = \frac{a}{b^2} 
\end{aligned}
$$

## 2. Beta Distribution ($x \in [0,1]$)

$$
\begin{aligned}
B(x|a,b) &= \frac{1}{B(a,b)} x^{a-1} (1-x)^{b-1} \\
& = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1} (1-x)^{b-1} \\
\end{aligned}
$$

Expectation:

$$
\begin{aligned}
\mathbb{E}[x] &= \int^1_0 x \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1} (1-x)^{b-1} \mathop{dx} \\
& = \int^1_0 \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a} (1-x)^{b-1} \mathop{dx} \\
& = \int^1_0 \frac{\Gamma(a+b+1)}{\Gamma(a+1)\Gamma(b)} \frac{a}{a+b} x^{a} (1-x)^{b-1} \mathop{dx} \\
& = \frac{a}{a+b} \int^1_0 B(x|a+1,b) \mathop{dx} \\
& = \frac{a}{a+b} \quad \text{(integral of pdf is 1)} \\
\end{aligned}
$$

Mode:

$$
\begin{aligned}
\mathrm{Mode}[x] & =  \mathrm{arg\,max}_x  \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1} (1-x)^{b-1} \\
i.e. \quad & \frac{\partial}{\partial x} x^{a-1} (1-x)^{b-1} = 0 \\
& (a-1) x^{a-2} (1-x)^{b-1} + (-1) (b-1) x^{a-1} (1-x)^{b-2} = 0 \\
& [(a-1)(1-x) - (b-1)x] x^{a-2} (1-x)^{b-2} = 0\\
& a - 1 - ax - bx + 2x = 0\\
\therefore \mathrm{Mode}[x] & = \frac{a-1}{a+b-2} \\
\end{aligned}
$$

Variance:

$$
\begin{aligned}
\mathrm{Var}[x] & = \int^1_0 x^2 \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1} (1-x)^{b-1} \mathop{dx}  - \mathbb{E}[x]^2 \\
& = \int^1_0 \frac{\Gamma(a+b+2)}{\Gamma(a+2)\Gamma(b)} \frac{a(a+1)}{(a+b)(a+b+1)} x^{a+1} (1-x)^{b-1} \mathop{dx}  - (\frac{a}{a+b} )^2 \\
& = \frac{a(a+1)}{(a+b)(a+b+1)}  - \frac{a^2}{(a+b)^2} \\
& = \frac{a(a+1)(a+b) - a^2(a+b+1)}{(a+b)^2(a+b+1)} \\
& = \frac{a[a(a+b) + (a+b) - a(a+b) - a)]}{(a+b)^2(a+b+1)} \\
& = \frac{ab}{(a+b)^2(a+b-1)}
\end{aligned}
$$

## 3. $\chi^2$ (Chi-squred) Distribution ($x \in [0,\infty)$)

For a set of independent, standard normal random variables $Z = \{z_1,...,z_k\} \sim \mathcal{N} (0, 1)$, the sum of their squares $Q = \sum^k_{i=1} z_i^2$ has the form of a chi-squared distribution with degrees of freedom $r = k$, i.e. $Q \sim \chi^2_k$ with the pdf:

$$
f(z | r) = \frac{z^{\frac{r}{2}-1} e^{-\frac{z}{2}}}{2^{\frac{r}{2}} \Gamma(\frac{r}{2})}
$$

### 3.1 $\chi^2$ and moment-generating functions

The moment-generating function of a random variable $X$ is:

$$
M_X(t) = \mathbb{E} [e^{tX}]
$$

This function can be used to find the moments of $X$ with the series expansion:

$$
\begin{aligned}
e^{tX} & = 1 + tX + \frac{t^2 X^2}{2!} + \frac{t^3 X^3}{3!} + ... \\
\text{Hence, } M_X(t) & =\mathbb{E} [e^{tX}]  = 1 + t m_1 + \frac{t^2 m_2}{2!} + \frac{t^3 m_3}{3!} + ...
\end{aligned}
$$

where $m_n$ is the $n$th moment.

If $X \sim \chi^2_r$, then:

$$
M_X(t) = (1 - 2t)^{-\frac{r}{2}}
$$


## 4.  Student's t-Distribution ($x \in (-\infty,\infty)$)

The pdf of the student's t-distribution is 

$$
f(t) = \frac{\Gamma(\frac{r+1}{2})}{\sqrt{r\pi} \Gamma(\frac{r}{2})}(1 + \frac{t^2}{r})^{-\frac{r+1}{2}}
$$

 where $r$ is the degree of freedom. 

To derive this pdf, we start from a sample of normally distributed population, $x = \{x_1,...,x_n\} \sim \mathcal{N}(\mu, \sigma^2)$. The random variable $t$ is then defined as:

$$
T = \frac{\bar X - \mu}{\frac{S}{\sqrt n}} \quad \text{where} \quad \bar X = \frac{1}{n} \sum^n_{i=1} x_i, \quad S^2 = \frac{1}{n-1} \sum^n_{i=1} (x_i - \bar X)^2
$$

Note that this results in a degree of freedom $v = n-1$. 

To derive the pdf of $T$, we need to first look at the relationship between $\bar X$ and $S$. We can prove that they are independent by checking the covariance between $\bar X$ and $x_i - \bar X$:

$$
\begin{aligned}
Cov(\bar X, x_i - \bar X) &= Cov(\bar X, x_i) - Cov(\bar X, \bar X) \\
& = \frac{1}{n} \sum^n_{i=1} Cov(x_i, x_j) - Var(\bar X) \\
& = \frac{1}{n} Cov(x_i, x_i) - \frac{1}{n} \sigma^2  \quad \text{Since samples of $X$ are independent} \\
& = \frac{1}{n} \sigma^2 - \frac{1}{n} \sigma^2 \\
& = 0
\end{aligned}
$$

Now, we can construct $f(t)$ using $f(\bar x)$ and $f(s)$. First, to find $f(\bar x)$, we apply z-score normalisation to $X$, thus getting a new standardised normal variable $Z = \sqrt n \frac{X - \mu}{\sigma}$. We can then compute:

$$
\begin{aligned}
f(\frac{\sqrt n (\bar x - \mu)}{\sigma}) = f(\bar z) \sim \mathcal{N} (0, 1) \text{ where } \bar Z = \frac{1}{n} \sum^n_{i=1} z_i
\end{aligned}
$$

We can also rewrite the variable $S$ into a new variable $U = \frac{(n-1)S^2}{\sigma^2}$. This gives us a new equivalent definition of $T$:

$$
T = \frac{\sigma \sqrt n (\bar X - \mu)}{\sigma} \frac{1}{\sqrt{S^2}} = \sigma \bar Z \sqrt{\frac{\sigma^2}{(n-1)S^2}} \sqrt{\frac{n-1}{\sigma^2}} = \frac{\bar Z}{\sqrt \frac{U}{(n-1)}}
$$

The rationale behind this substitution is that it allows us to express $S$ in the standardised normal variable $Z$. This helps us to find $f(s)$ using properties of the $\chi^2$ distribution. First we can decompose $U$ into the sum of two $\chi^2$ distributed terms:

$$
\begin{aligned}
U & = \frac{(n-1)S^2}{\sigma^2} = \frac{1}{\sigma^2} \sum^n_{i=1} (x_i - \bar X)^2 = \sum^n_{i=1} (z_i - \bar Z)^2 \\
& = \sum^n_{i=1} z_i^2 - 2 \sum^n_{i=1} z_i \bar Z+ \sum^n_{i=1} \bar Z^2 \\
& = \sum^n_{i=1} z_i^2 - 2 (n \bar Z) \bar Z + n \bar Z^2 \\
& = \sum^n_{i=1} z_i^2  - n \bar Z^2 \\
& \text{where } \sum^n_{i=1} z_i^2 \sim \chi^2_n, \quad \sum^n_{i=1} \bar Z^2 = n \bar Z^2 \sim \chi^2_1
\end{aligned}
$$

We can make use of the moment-generating function of these two $\chi^2$ variables to find that of $U$. Moment-generating function of linear combination of independent random variables is the product/division of their moment-generating functions, i.e.:

$$
\begin{aligned}
\text{For } U  & = \sum^n_{i=1} z_i^2 - n \bar Z^2 = Y - V,  \quad M_U(t) = \frac{M_Y(t)}{M_V(t)} \\
& \therefore M_U(t)  = \frac{(1 - 2t)^{-\frac{n}{2}}}{(1 - 2t)^{-\frac{1}{2}}} = (1 - 2t)^{-\frac{n-1}{2}}
\end{aligned}
$$

This means that $U$ also follows the $\chi^2$ distribution, and with a degree of freedom $r = n-1$.

Now we can express the pdf of $\bar Z$ and $U$, as well as their joint pdf:

$$
\begin{aligned}
f_{\bar Z}(\bar z) & = \frac{1}{\sqrt{2\pi}} e^{-\frac{\bar z^2}{2}}, \quad f_U(u) = \frac{u^{\frac{n-1}{2}-1} e^{-\frac{u}{2}}}{2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} \\
f_{\bar Z,U}(\bar z,u) & = f_{\bar Z}(\bar z)f_U(u) = \frac{u^{\frac{n-1}{2}-1}}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} e^{-\frac{\bar z^2}{2} - \frac{u}{2}}
\end{aligned}
$$

Now, we can substitute $t$ into the pdf with a change of variable with $z$:

$$
\begin{aligned}
\text{Since } & T = \frac{\bar Z}{\sqrt \frac{U}{(n-1)}} \text{, then } \bar Z = T \sqrt \frac{U}{(n-1)}\\
f_{T,U}(t,u) & = f_{\bar Z,U}(t \sqrt \frac{u}{(n-1)},u) | J(t, u) | \\
& = \frac{u^{\frac{n-1}{2}-1}}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} e^{-\frac{1}{2} [(t \sqrt \frac{u}{(n-1)})^2 + u]} | det \begin{bmatrix} \frac{\partial \bar z}{\partial t} & \frac{\partial \bar z}{\partial u} \\ \frac{\partial u}{\partial t} & \frac{\partial u}{\partial u} \\ \end{bmatrix} | \\
& = \frac{1}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} u^{\frac{n-3}{2}} e^{-\frac{1}{2} (\frac{t^2 u}{(n-1)} + u)} | det \begin{bmatrix} \sqrt \frac{u}{(n-1)} & \frac{t}{2 \sqrt{u (n-1)}} \\ \ 0 & 1 \\ \end{bmatrix} | \\
& = \frac{1}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} u^{\frac{n-3}{2}} e^{-\frac{1}{2} u (\frac{t^2}{(n-1)} + 1)} \sqrt \frac{u}{(n-1)}  \\
\therefore f_T(t) & = \int^\infty_0 f_{T,U}(t,u) \mathop{du} = \int^\infty_0 \frac{1}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2})} u^{\frac{n-3}{2}} e^{-\frac{1}{2} u (\frac{t^2}{(n-1)} + 1)} \sqrt \frac{u}{(n-1)} \mathop{du} \\
& = \frac{1}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2}) \sqrt{(n-1)}} \int^\infty_0 u^{\frac{n}{2}-1} e^{-\frac{1}{2} u (\frac{t^2}{(n-1)} + 1)} \mathop{du} \\
& = \frac{1}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2}) \sqrt{(n-1)}} \int^\infty_0 (\frac{2w}{\frac{t^2}{(n-1)} + 1})^{\frac{n}{2}-1} e^{-w} \frac{du}{dw} \mathop{dw} \text{, where } w = \frac{u}{2} (\frac{t^2}{(n-1)} + 1) \\
& = \frac{2^{\frac{n}{2}-1} (\frac{t^2}{(n-1)} + 1)^{-\frac{n}{2}+1}}{\sqrt{2\pi} 2^{\frac{n-1}{2}} \Gamma(\frac{n-1}{2}) \sqrt{(n-1)}} \int^\infty_0 w^{\frac{n}{2}-1} e^{-w} (\frac{2}{\frac{t^2}{(n-1)} + 1}) \mathop{dw} \\
& = \frac{(\frac{t^2}{(n-1)} + 1)^{-\frac{n}{2}}}{\sqrt{\pi} \Gamma(\frac{n-1}{2}) \sqrt{(n-1)}} \int^\infty_0 w^{\frac{n}{2}-1}  e^{-w} \mathop{dw} \\
& = \frac{ (\frac{t^2}{(n-1)} + 1)^{-\frac{n}{2}}}{\sqrt{\pi} \Gamma(\frac{n-1}{2}) \sqrt{(n-1)}} \Gamma(\frac{n}{2}) \\
& = \frac{ \Gamma(\frac{n}{2})}{\sqrt{(n-1) \pi} \Gamma(\frac{n-1}{2})} (\frac{t^2}{(n-1)} + 1)^{-\frac{n}{2}}  \\
& = \frac{ \Gamma(\frac{r+1}{2})}{\sqrt{r \pi} \Gamma(\frac{r}{2})} (1 + \frac{t^2}{r})^{-\frac{r+1}{2}}  \text{ for } r = n-1\\
\end{aligned}
$$

