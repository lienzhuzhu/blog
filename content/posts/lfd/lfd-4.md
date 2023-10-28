+++
title = "Learning From Data Problem Set 4"
date = "2023-10-26T21:18:07-07:00"
# description = ""

tags = ["notes", "ml"]
+++

Below are my solutions to the self-paced version of Caltech's CS 156 Machine Learning course. [PDF of problems](https://work.caltech.edu/homework/hw4.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)

**1. [d]**

I made a small script to do the iterative calculation:

```
❯ python3 hw4/sample-complexity.py
452955.4551979035
```


**2. [d]**

For problems 2 and 3 we need to find an explicit form for the Parrondo and Van den Broek and Devroye bounds.

First, recall the quadratic formula as we will use it later.

$$
\frac{-b \pm \sqrt{b^2-4ac}}{2a}
$$

_Parrondo and Van den Broek_

$$
\begin{aligned}
\epsilon    &   \leq    \sqrt{\frac{1}{N}(2\epsilon + \ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}})} \\\ \\\
\epsilon^2  &   \leq    \frac{1}{N}(2\epsilon + \ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}) \\\ \\\
\epsilon^2 - \frac{2}{N}\epsilon - \frac{1}{N}\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}    & \leq  0 \\\ \\\
\end{aligned}
$$

Now we apply the quadratic formula. Let's first make clear what the values will be:

$$
\begin{aligned}
a &= 1 \\\ \\\
b &= -\frac{2}{N} \\\ \\\
c &= -\frac{1}{N}\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}
\end{aligned}
$$

Now we can get to work:

$$
\begin{aligned}
\epsilon    & = \frac{\frac{2}{N} \pm \sqrt{(\frac{2}{N})^2 + 4 \cdot \frac{1}{N}\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}}}{2} \\\ \\\
            & = \frac{1}{N} \pm \frac{1}{N}\sqrt{1+N\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}}
\end{aligned}
$$

We note that the quadratic opens upward since $a > 0$. That means that for $\epsilon$ between the two solutions from each side of the $\pm$, the quadratic will be less than zero. That is

$$
\epsilon_1 \leq \epsilon \leq \epsilon_2
$$

if $\epsilon_1$ is the solution from the minus and $\epsilon_2$ is the solution from the positive. We only care about an upper bound on $\epsilon$, so we have

$$
\epsilon \leq \frac{1}{N} + \frac{1}{N}\sqrt{1+N\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}}
$$

We need to substitute in the bound on $m_{\mathcal{H}} \leq N^{d_{vc}}$:

$$
\epsilon \leq \frac{1}{N} + \frac{1}{N}\sqrt{1+N\ln{\frac{6m_{\mathcal{H}}(2N)}{\delta}}}
$$

becomes

$$
\epsilon \leq \frac{1}{N} + \frac{1}{N}\sqrt{1+N\ln{\frac{6((2N)^{d_{vc}} + 1)}{\delta}}}
$$


This is the form of the Parrondo and Van den Broek generalization bound that we will use later. $\blacksquare$


_Devroye_

$$
\begin{aligned}
\epsilon        & \leq  \sqrt{\frac{1}{2N}(4\epsilon(1+\epsilon) + \ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}})} \\\ \\\
\epsilon^2      & \leq  \frac{1}{2N}(4\epsilon(1+\epsilon) + \ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}) \\\ \\\
\epsilon^2      & \leq  \frac{1}{2N}(4\epsilon + 4\epsilon^2 + \ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}) \\\ \\\
\epsilon^2      & \leq  \frac{4}{2N}\epsilon + \frac{4}{2N}\epsilon^2 + \frac{1}{2N}\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}} \\\ \\\
(1-\frac{2}{N})\epsilon^2 - \frac{2}{N}\epsilon - \frac{1}{2N}\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}     & \leq  0 \\\ \\\
\end{aligned}
$$

Now we are ready to use the quadratic equation with

$$
\begin{aligned}
a   & = 1-\frac{2}{N} \\\ \\\
b   & = -\frac{2}{N} \\\ \\\
c   & = -\frac{1}{2N}\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}
\end{aligned}
$$

which yields

$$
\begin{aligned}
\epsilon    & = \frac{\frac{2}{N} \pm \sqrt{(\frac{2}{N})^2 + 4(1-\frac{2}{N})\frac{1}{2N}\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}}}{2(1-\frac{2}{N})} \\\ \\\
            & = \frac{ \frac{2}{N} \pm \sqrt{ (\frac{2}{N})^2 + (\frac{2}{N} - (\frac{2}{N})^2)\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}}}{2-2\cdot\frac{2}{N}} \\\ \\\
            & = \frac{ \frac{2}{N} \pm \frac{2}{N}\sqrt{ (1 + (\frac{N}{2}-1)\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}}}{\frac{2}{N}(N-2)} \\\ \\\
            & = \frac{ 1 \pm \sqrt{ (1 + (\frac{N}{2}-1)\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}}}{N-2} \\\ \\\
            & = \frac{ 2 \pm \sqrt{ (4 + (2N-4)\ln{\frac{4m_{\mathcal{H}}(N^2)}{\delta}}}}{2N-4} \\\ \\\
\end{aligned}
$$


I won't explain it here but again we only care about the plus side of the solution pair. We will have to take special care when substituting in the polynomial bound on the growth function for this bound to avoid overflow. 

$$
\begin{aligned}
\frac{ 2 \pm \sqrt{ (4 + (2N-4)\ln{\frac{4((N^2)^{d_{vc}} + 1)}{\delta}}}}{2N-4}    & =         \frac{ 2 \pm \sqrt{ 4 + (2N-4)( \ln{ \frac{4}{\delta} } + \ln{ \frac{N^{2d_{vc}}+1}{\delta}})}}{2N-4}  \\\ \\\
                                                                                    & \approx   \frac{ 2 \pm \sqrt{ (4 + (2N-4)(\ln{\frac{4}{\delta}} + 2d_{vc}\ln{N} - \ln{\delta})}}{2N-4}
\end{aligned}
$$

The approximation is necessary for later when we implement this in code so the program doesn't overflow. $\blacksquare$


We use these bounds in `hw4/bounds.py`.

For large $N$, `python3 hw4/bounds.py` shows that the Devroye bound is the smallest.

```
❯ python3 hw4/bounds.py -N 10000
VC Bound                         0.632174915200836
Rademacher                       0.3313087859616395
Parrondo and Van den Broek       0.2236982936807856
Devroye                          0.2155759485446348
```


**3. [c]**

```
❯ python3 hw4/bounds.py -N 5
VC Bound                         13.828161484991483
Rademacher                       7.048776564183685
Parrondo and Van den Broek       5.101361981989993
Devroye                          5.629897473598194
```


**4. [e]**

Use the code linked at the start of the post.

`python3 hw4/bias.py` shows the average hypothesis has a slope of $1.43$.


**5. [b]**

The bias for this $\bar{g}(x)$ is likely the same as the $\bar{g}(x)$ for $\mathcal{H}_1$ in the book since they seem to be the same form. Of course, this $\mathcal{H}$ where each $h \in \mathcal{H}$ does not have the $y$-intercept parameter and so we would expect its variance to be smaller than that for $\mathcal{H}_1$


**6. [a]**

The maximum slope that $a$ could equal is $\pi$, while the most negative slope is $0$. If the line that goes through $x_1$ and $x_2$ would have a negative slope, the line of best fit through the origin will still have a positive slope less than $\pi$! So we can conclude that if you spin a line about the origin such that it has a slope of $0$ and $\pi$ and everything in between, you can convince yourself it doesn't vary nearly as much as the $\bar{g}(x)$ for $\mathcal{H}_1$, and is going to be close to the variance for $\bar{g}(x)$ of $\mathcal{H}_0$.


**7. [b]**

We use the principle explicitly stated in the lectures: "Match the model complexity to the data resources available".

$h(x) = b$ is too simple, so it has a high bias. $h(x) = ax + b$ achieves better bias with some added model complexity, but this increase in model complexity introduces a killer variance of $1.69$! It is already too complex for this data set, as will any quadratic form. It seems $h(x) = ax$ is the optimal choice out of these options.
