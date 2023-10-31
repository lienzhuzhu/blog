+++
title = "Learning From Data Problem Set 5"
date = "2023-10-27T23:13:23-07:00"
# description = ""

tags = ["notes"]
+++

[PDF of problems](https://work.caltech.edu/homework/hw5.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)


<h3>1. [c]</h3>

Plugging in the values for $\mathbb{E}[E_{in}(\vec{w})] = \sigma^{2}(1 - \frac{d+1}{N}) \geq 0.008$:

$$
\begin{aligned}
\mathbb{E}[E_{in}(\vec{w})]     & =     \sigma^{2}(1 - \frac{d+1}{N}) \\\ \\\
                                & =     (0.1)^2(1 - \frac{9}{N}) \\\ \\\
0.01 - \frac{0.09}{N}           & \geq  0.008 \\\ \\\
0.002                           & \geq  \frac{0.09}{N} \\\ \\\
N                               & \geq  \frac{0.09}{0.002} \\\ \\\
N                               & \geq  45
\end{aligned}
$$


<h3>2. [d]</h3>

We need to think about how the features affect the labels of the regions.

For any given point, it seems the closer it is to the $x_1 = 0$ line, the more it tends to be positively labeled, so being further away is an attribute that would label it more negatively. So having $\tilde{w}\_1 < 0$ makes sense.

It also seems the further away from $x_2 = 0$ a point is, the more it tends to be positively labeled, especially if we compare the size of the regions going up and down to infinity. So $\tilde{w}\_2 > 0$.


<h3>3. [c]</h3>

Use the formula $\frac{Q(Q+3)}{2}$ with $Q=4$.


<h3>4. [e]</h3>

Just use chain rule.

$$
\begin{aligned}
\frac{\partial{E}}{\partial{u}} &= \frac{\partial{E}}{\partial{u}}(ue^v-2ve^{-u})^2 \\\ \\\
    &= 2(ue^v - 2ve^{-u})(e^v + 2ve^{-u})
$$
\end{aligned}
