+++
title = "Learning From Data Problem Set 3"
date = "2023-10-23T19:14:38-07:00"
# description = ""

tags = ["notes"]
+++


Below are my solutions to self-paced version of the Caltech CS 156 Learning From Data course.


**1. [b]**

We can express our confidence as $\delta = 2Me^{-2\epsilon^2N}$ and manipulate this expression to put it in terms of $N$:

$$
\begin{aligned}
2Me^{-2\epsilon^2N} & = \delta \\\ \\\
e^{-2\epsilon^2N}   & = \frac{\delta}{2M} \\\ \\\
-2\epsilon^2N       & = \ln{\frac{\delta}{2M}} \\\ \\\
N                   & = \frac{1}{2\epsilon^2}\ln{\frac{2M}{\delta}}
\end{aligned}
$$

Then for the next 3 problems we can use this expression by plugging in for $M$, $\delta$, and $\epsilon$:

$\epsilon = 0.05$
$\delta = 0.03$

For $M = 1$:
$$
\begin{aligned}
N   & =         \frac{1}{2\epsilon^2}\ln{\frac{2}{\delta}} \\\ \\\
    & \approx   840 
\end{aligned}
$$

For $M = 10$:
$$
\begin{aligned}
N   & =         \frac{1}{2\epsilon^2}\ln{\frac{20}{\delta}} \\\ \\\
    & \approx   1300 
\end{aligned}
$$

For $M = 100$:
$$
\begin{aligned}
N   & =         \frac{1}{2\epsilon^2}\ln{\frac{200}{\delta}} \\\ \\\
    & \approx   1761 
\end{aligned}
$$


**4. [b]**

The way to ensure the arrangement of points doesn't limit the number of potential dichotomies is to arrange them such that no more than 3 points are colinear and no more than 4 are co-planar. I like to check pairs of points and see if I can separate them from the other $N-2$ points.

For 4 points in $\mathbb{R}^3$, we can separate any pair of points from the others if we imagine a tetrahedron. 

For 5 points in $\mathbb{R}^3$, we arrange the points into a pentahedron, with the base slightly distorted. Observe that no matter what plane you imagine, 2 points that are diagonal from each other in the base can never be alone together. You can try to distort the base to get your intended points alone together, but that would just make it so the other pair of points that make up the base cannot be alone together!


