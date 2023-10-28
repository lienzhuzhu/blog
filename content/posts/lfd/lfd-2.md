+++
title = "Learning From Data Problem Set 2"
date = "2023-10-20T18:25:47-07:00"
# description = ""

tags = ["notes", "ml"]
+++


[PDF of problems](https://https://work.caltech.edu/homework/hw2.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)


Refer to the code repository above for problems 1 and 2. Usage: `python3 hw2/coin.py`.

**1. [b]**

I get something in the range $[0.03, 0.04]$ for the average value of $\nu_{min}$ so the correct answer is pretty close to being 0.1 but alas it is still correct to say 0.01.


**2. [d]**

The graphs show us that the $c_{min}$ coin is not bounded by the Hoeffding bound as we would expect. This makes sense because the Hoeffding inequality only applies to situations where we decide on a strategy before working on the data. In the learning problem, we pick $g$ based on the performance of many $h$'s on the dataset.


**3. [e]**

The key point of the concept of noise is that sometimes $y \neq f(\vec{x})$, or in other words, $y$ does not correspond the $f(\vec{x})$ completely. 

We want to find $P(h(\vec{x}) \neq y)$. We know that $y = f(\vec{x})$ with probability $\lambda$ and does not match $f(\vec{x})$ with a probability of $1-\lambda$. We want to add together the probabilities of the instances where $h(\vec{x}) \neq y$, which is when $h(\vec{x}) = f(\vec{x})$ but $y \neq f(\vec{x})$, and $h(\vec{x}) \neq f(\vec{x})$ but $y = f(\vec{x})$.

Now that we've broken the question down, it becomes easier to put some math to it:

$$
\begin{aligned}
P(h(\vec{x}) \neq y)    & = P(y = f(\vec{x}) \cap h(\vec{x}) \neq f(\vec{x})) + P(y \neq f(\vec{x}) \cap h(\vec{x}) = f(\vec{x})) \\\
                        & = \lambda \mu + (1-\lambda)(1-\mu)
\end{aligned}
$$


**4. [b]**

When $\lambda = 0.5$, the correspondence between $y$ and $f(\vec{x})$ is basically random.



For 5-7, use the code linked at the top of this post.

**5. [c]**

`python3 hw2/2linregression.py -N 100` yields somewhere around $[0.03, 0.04]$ for me.

**6. [c]**

`python3 hw2/linregression.py -N 100` yields somewhere around $[0.04, 0.05)$ for me.

**7. [a]**

`python3 hw2/linregression.py -N 10` yields somewhere around $[3, 7]$ for me.


For 8-10, use the code linked at the top of this post.

**8. [d]**
`python3 hw2/transform.py -N 1000` has E_in really close to $0.5$.

**9. [a]**
`python3 hw2/transform.py -N 1000` has the $1.5$ coefficients on the last two terms which affect the result the most, so I selected [a].

**10. [b]**
I get around $0.12$
