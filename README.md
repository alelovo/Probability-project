# Binary Signal Recovery Using the Metropolis-Hastings Algorithm

-------------------------------------------------------------------

This is my final project for the Probability course, University of Verona, Academic Year 2023/2024.

-------------------------------------------------------------------

The **scope of the present project** is to illustrate **how to recover a binary signal from noisy observations using Markov Chain Monte Carlo techniques, Metropolis-Hastings Algorithm. **


# **Starting Point** 


**Mathematical Model**

Let:

*  $\mathbf{X} \in \mathbb{R}^{m \times d}$ be a random matrix with i.i.d. entries drawn from $\mathcal{N}(0,1)$.
*  $\boldsymbol{\xi} \in \mathbb{R}^m$ be a noise vector with i.i.d. entries drawn from $\mathcal{N}(0,1)$, independent of $\mathbf{X}$.
*  $\Theta = \{0,1\}^d$ be the signal space.
*  $\boldsymbol{\theta} \in \Theta$ be a signal chosen uniformly at random, independent of $(\mathbf{X}, \boldsymbol{\xi})$.

The measurement vector $\mathbf{y} \in \mathbb{R}^m$ is generated as:

$$\mathbf{y} = \mathbf{X} \boldsymbol{\theta} + \boldsymbol{\xi}$$

we can see as:

$\theta$ represents a binary signal that we want to transmit or recover. The matrix $\mathbf{X}$ could represent a sensor system that detects the signal, while $\boldsymbol{\xi}$ represents the noise that inevitably introduces itself into the measurement process. The result $\mathbf{y}$ is therefore what the sensors detect, a mix of the true signal and the noise.

**The objective is to estimate a binary parameter vector $\theta$ from noisy observations $y$.**

## **Maximum likelihood estimation**

"It provides a measure of the plausibility of each parameter value, given the observed sample, and takes higher values for more plausible parameter values."

So we have to find the **vector $\theta$ that maximizes the likelihood of the observations $y$.**

$\mathcal{H}(X, y; \theta) = (y - X\theta)^T (y - X\theta)$

## **Metropolis-Hastings Algorithm**

Why we use it in this problem ?

is used to sample from a complex probability distribution, in this case, to find the maximum likelihood estimator. This **method is useful when the parameter space is large**, and the objective function (the likelihood function) is difficult to optimize directly.

The stationary distribution $\pi_{\beta}(\theta)$ is defined as:

$\pi_{\beta}(\theta) = \frac{e^{-\beta H(X;y;\theta)}}{Z_{\beta}}, \quad \text{with} \quad Z_{\beta} = \sum_{\theta \in \Theta} e^{-\beta H(X;y;\theta)}$

$\pi_{\beta}(\theta)$ is a probability distribution over the possible states $\theta$ in your state space $\Theta$.







