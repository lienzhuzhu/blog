+++
title = "CS 156 Learning From Data Notes"
date = "2023-10-21T11:01:49-07:00"
# description = ""

tags = ["notes"]
+++


<h3>Loosening the Hoeffding Inequality for $g$</h3>

The Hoeffding Inequality for any particular hypothesis $h$ bounds the deviation between $E_{in}$ and $E_{out}$:

$$
\mathbb{P}(|E_{in}(h) - E_{out}(h)| > \epsilon) \leq 2e^{-2\epsilon^2N}
$$


When bounding the approximation of $E_{out}(g)$ by $E_{in}(g)$, we cannot just plug in $g$ for $h$. This is because $g$ is selected after applying the hypothesis set $\mathcal{H}$ onto the data, so $g$ is cherry-picked based on performance of the hypotheses. 

Instead, we have to use the implication and addition rule of probability. 

If $A \implies B$, then $\mathbb{P}(A) \leq \mathbb{P}(B)$, since event $B$ always occurs whenever $A$ occurs, but may also occur when $A$ does not occur.

Also, $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$ by the addition rule of probability. In fact, we can derive what's called the _Union Bound_ from this rule:

$$
\begin{aligned}
\mathbb{P}(A \cup B)    & =     \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B) \\\
                        & \leq  \mathbb{P}(A) + \mathbb{P}(B)
\end{aligned}
$$

Basically, if $A$ and $B$ are disjoint, then by definition $\mathbb{P}(A \cap B) = 0$, _i.e._ there is not overlap between $A$ and $B$. This means in general, the union of any two events, disjoint or not, is less than or equal the probability of the disjoint case.

Because $g$ is one of the $h_M$'s, we know this implication holds true:

$$
|E_{in}(g) - E_{out}(g)| > \epsilon \quad\implies\quad |E_{in}(h_1) - E_{out}(h_1)| > \epsilon \textbf{ or } |E_{in}(h_2) - E_{out}(h_2)| > \epsilon \dots \textbf{ or } |E_{in}(h_M) - E_{out}(h_M)| > \epsilon \\\ \\\
$$

$$
\therefore \mathbb{P}(|E_{in}(g) - E_{out}(g)| > \epsilon) \quad\leq\quad \mathbb{P}[|E_{in}(h_1) - E_{out}(h_1)| > \epsilon \textbf{ or } |E_{in}(h_2) - E_{out}(h_2)| > \epsilon \dots \textbf{ or } |E_{in}(h_M) - E_{out}(h_M)| > \epsilon]
$$

The RHS of that expression follows the addition rule:

$$
\begin{aligned}
\mathbb{P}[|E_{in}(h_1) - E_{out}(h_1)| > \epsilon \textbf{ or } |E_{in}(h_2) - E_{out}(h_2)| > \epsilon \dots \textbf{ or } |E_{in}(h_M) - E_{out}(h_M)| > \epsilon]   & \quad\leq\quad    \sum_{m=1}^{M}\mathbb{P}(|E_{in}(h_m) - E_{out}(h_m)| > \epsilon) \\\ \\\
                                                                                                                                                                        & \quad=\quad       2Me^{-2\epsilon^2N}
\end{aligned}
$$


Which leaves us with
$$
\mathbb{P}(|E_{in}(g) - E_{out}(g)| > \epsilon) \quad\leq\quad 2Me^{-2\epsilon^2N} \quad\blacksquare
$$

We can already see that if the cardinality of the hypothesis space, $|\mathcal{H}| = M$, is infinite, the bound is useless, it is too loose because it considers the worst case that no hypotheses will overlap in their classifications on $\mathcal{D}$. In reality, for any given $\mathcal{D}$, many hypotheses will output the same classifications. Take for instance the perceptron and let's say we have two points, one of which is $+1$ the other $-1$. There are basically an infinite number of $h$'s that would classify these two examples in $\mathcal{D}$ correctly!

Later, we'll see how we can tighten this bound by taking into account these overlapping, or effectively equal, hypotheses.