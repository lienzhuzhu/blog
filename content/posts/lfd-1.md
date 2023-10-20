+++
title = "Learning From Data Problem Set 1"
date = "2023-10-19T19:49:57-07:00"
# description = ""

tags = ["notes"]
+++


Below are my solutions to the self-paced version of the Learning From Data course at Caltech.


**1. [d]**

Scenario $(\texttt{i})$ is a design problem. Scenario $(\texttt{ii})$ is the typical supervised learning problem like the perceptron introduced in the first chapter. Scenario $(\texttt{iii})$ describes a reinforcement learning because it describes an agent learning to play a game with a reward or cost function.


**2. [a]**

$(\texttt{i})$ and $(\texttt{iii})$ describe problems where a mathematical equation can be found to describe the solution. So by process of elimination, the answer is [a].


**3. [d]**

This is a conditional probability and Baye's theorem problem with perhaps one more layer than most introductory stats classes will ask about because the probability of drawing a second black ball is dependent on the initial selection of a bag.

We have:

$$
P(\textrm{Second ball drawn is black } | \textrm{ First ball drawn is black}) = \frac{P(\textrm{Second ball drawn is black } \cap \textrm{ First ball drawn is black})}{P(\textrm{First ball drawn is black})}
$$


Okay, so what is the probability of drawing two black balls in a row? Well, the bag chosen must be the one with two black, which has a probability of $\frac{1}{2}$ of being chosen, then the probability from that point is 1. So the probability along that branch is $\frac{1}{2} \cdot 1$

The probability of drawing a black ball on the first draw is $\frac{1}{2} \cdot 1 + \frac{1}{2} \cdot \frac{1}{2}$. The first term is the same as the previous calculation, and the second term comes from the probability of drawing a black ball after choosing the half and half bag.

All together now:

$$
\begin{aligned}
P(\textrm{Second ball drawn is black } | \textrm{ First ball drawn is black})   & = \frac{\frac{1}{2}}{\frac{1}{2} \cdot 1 + \frac{1}{2} \cdot \frac{1}{2}} \\\ \\\
                                                                                & = \frac{2}{3}
\end{aligned}
$$


**4. [b]**

Use binomial distribution. Let $X \sim \text{Binom}(10, 0.55)$. Then the $P(X = 0)$ can be calculated:

$$
\begin{aligned}
P(X = 0)    & = \binom{10}{0}(0.55)^0(0.45)^10 \\\ \\\
            & = 3.405 \times 10^{-4}
\end{aligned}
$$


**5. [c]**

We again have to use binomial distribution, but craft our random variable carefully. We have to zoom out and rethink our definition of a Bernoulli trial. Let's have $Y$ be the number of samples (or experiments) of 10 marble draws that have a $\nu$ of 0, in other words, 0 red marbles out of 10 drawn.

Then, we can have $Y \sim \text{Binom}(1000, 3.405 \times 10^{-4})$ since we calculated the probability of any one sample having 0 red marbles out of 10 in the last problem.

$$
\begin{aligned}
P(Y \geq 1) & = 1 - P(Y = 0) \\\ \\\
            & = 1 - \binom{1000}{0}(3.405 \times 10^{-4})^0(1 - 3.405 \times 10^{-4})^{1000} \\\ \\\
            & = 0.2886
\end{aligned}
$$


**6. **
