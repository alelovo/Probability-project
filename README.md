# Binary Signal Recovery Using the Metropolis-Hastings Algorithm

-------------------------------------------------------------------

This is my final project for the Probability course, University of Verona, Academic Year 2023/2024.

-------------------------------------------------------------------

The **scope of the present project** is to illustrate **how to recover a binary signal from noisy observations using Markov Chain Monte Carlo techniques.**


# **Starting Point** 


**Mathematical Model**

## 1. how can we generate data:

Let:

*  $\mathbf{X} \in \mathbb{R}^{m \times d}$ be a random matrix with i.i.d. entries drawn from $\mathcal{N}(0,1)$.
*  $\boldsymbol{\xi} \in \mathbb{R}^m$ be a noise vector with i.i.d. entries drawn from $\mathcal{N}(0,1)$, independent of $\mathbf{X}$.
*  $\Theta = \{0,1\}^d$ be the signal space.
*  $\boldsymbol{\theta} \in \Theta$ be a signal chosen uniformly at random, independent of $(\mathbf{X}, \boldsymbol{\xi})$.

we can see as:

$\theta$ represents a binary signal that we want to transmit or recover. The matrix $\mathbf{X}$ could represent a sensor system that detects the signal, while $\boldsymbol{\xi}$ represents the noise that inevitably introduces itself into the measurement process. The result $\mathbf{y}$ is therefore what the sensors detect, a mix of the true signal and the noise.

## 2. How can we estimate $\boldsymbol{\theta} \in \Theta$ ?

* **Maximum likelihood estimation**

"It provides a measure of the plausibility of each parameter value, given the observed sample, and takes higher values for more plausible parameter values."

So we have to find the **vector $\theta$ that maximizes the likelihood of the observations $y$.**

The maximum likelihood estimate $ \hat{\theta} $ is given by the value of $ \theta $ that maximizes the likelihood function:

$\mathcal{L}(X, y; \theta) = \frac{\exp \left\{-\frac{1}{2} (y - X\theta)^T (y - X\theta)\right\}}{(2\pi)^{m/2}}$

which is equivalent to minimizing the function $\log L(X, y; \theta) = -\frac{1}{2} (y - X\theta)^T (y - X\theta) - \frac{m}{2} \log(2\pi)
$


##3. Metropolis-Hastings Algorithm

Why we use it in this problem ?

is used to sample from a complex probability distribution, in this case, to find the maximum likelihood estimator $\hat{\theta}$. This **method is useful when the parameter space is large** ($\Theta = \{0,1\}^d$), and the objective function (the likelihood function) is difficult to optimize directly.


* **Explore the Solution Space**: The algorithm samples different candidate vectors $\theta$.

* **Maximize the Likelihood**: It finds the vector $\theta$ that minimizes the quadratic error between $\mathbf{y}$ and $\mathbf{X} \theta$.

So we construct the Metropolis-Hastings (discrete-time) Markov
chain, with:

The stationary distribution $ \pi_{\beta}(\theta) $ is defined as:

$ \pi_{\beta}(\theta) = \frac{e^{-\beta H(X;y;\theta)}}{Z_{\beta}}, \quad \text{with} \quad Z_{\beta} = \sum_{\theta \in \Theta} e^{-\beta H(X;y;\theta)}$

$\pi_{\beta}(\theta)$ is a probability distribution over the possible states $\theta$ in your state space $\Theta$.


**The structure of the Markov chain we obtain with the Metropolis-Hastings algorithm is characterized by:**

* **States**: Each state represents a possible configuration of the vector $\theta$.

* **Convergence**: After a sufficient number of iterations, the chain converges to the maximum likelihood distribution, MLE $\hat{\theta}$.
Also with $\beta$ large enough.

## 4. Now we have to we analyze the **mean squared error**

In order to check the quality of our estimation:

$$
\xi = \mathbb{E}\left[ (\hat{\theta} - \theta)^T (\hat{\theta} - \theta) \right]
\quad
$$

**Why we use the MSE in this problem?**

* **PERFORMANCE EVALUATION**: how well the estimated $\theta_{est} $ vector approximates the true $\theta_{true}$ vector.

* **MEASURE ACCURACY**: provides a single numerical value representing the sum of the squared deviations of the estimates from the true values. Smaller MSE values indicate that the estimated vector is closer to the true vector, meaning the algorithm performed well.


## 5. **Algorithm procedure**

1. Set $\boldsymbol{\theta}_0 = \bar{\boldsymbol{\theta}}$.
2. For $t = 1, 2, \ldots, N - 1$:
   1. Pick $i$ uniformly at random in $\{1, 2, \ldots, d\}$.
   2. Let the proposed state be $\boldsymbol{\theta}^* \in \Theta$, with entries $\boldsymbol{\theta}^*(j) = $
      \begin{cases}
          \boldsymbol{\theta}^{t-1}(j) & \text{if } j \neq i \\
          1 - \boldsymbol{\theta}^{t-1}(j) & \text{if } j = i
      \end{cases}
    
    for $ j = 1, 2, \ldots, d. $
   3. Set
      $\boldsymbol{\theta}^t = $
      
      \begin{cases}
          \boldsymbol{\theta}^* & \text{with probability } \min\left\{1, \frac{\exp\{-\beta H(\mathbf{X}, \mathbf{y}; \boldsymbol{\theta}^*)\}}{\exp\{-\beta H(\mathbf{X}, \mathbf{y}; \boldsymbol{\theta}^{t-1})\}}\right\} \\
          \boldsymbol{\theta}^{t-1} & \text{with probability } 1 - \min\left\{1, \frac{\exp\{-\beta H(\mathbf{X}, \mathbf{y}; \boldsymbol{\theta}^*)\}}{\exp\{-\beta H(\mathbf{X}, \mathbf{y}; \boldsymbol{\theta}^{t-1})\}}\right\}
      \end{cases}
