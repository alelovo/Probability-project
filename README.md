# Binary Signal Recovery Using the Metropolis-Hastings Algorithm

-------------------------------------------------------------------

This is my final project for the Probability course, University of Verona, Academic Year 2023/2024.

-------------------------------------------------------------------

The **scope of the present project** is to illustrate **how to recover a binary signal from noisy observations using Markov Chain Monte Carlo techniques.**


# **Starting Point** 


**Mathematical Model**

Let:

*  $\mathbf{X} \in \mathbb{R}^{m \times d}$ be a random matrix with i.i.d. entries drawn from $\mathcal{N}(0,1)$.
*  $\boldsymbol{\xi} \in \mathbb{R}^m$ be a noise vector with i.i.d. entries drawn from $\mathcal{N}(0,1)$, independent of $\mathbf{X}$.
*  $\Theta = \{0,1\}^d$ be the signal space.
*  $\boldsymbol{\theta} \in \Theta$ be a signal chosen uniformly at random, independent of $(\mathbf{X}, \boldsymbol{\xi})$.

we can see as:

$\theta$ represents a binary signal that we want to transmit or recover. The matrix $\mathbf{X}$ could represent a sensor system that detects the signal, while $\boldsymbol{\xi}$ represents the noise that inevitably introduces itself into the measurement process. The result $\mathbf{y}$ is therefore what the sensors detect, a mix of the true signal and the noise.

