+++
title = "Learning From Data Book Notes"
date = "2023-10-18T19:49:57-07:00"
# description = ""

tags = ["notes"]
+++


<h3>Loosening the Hoeffding Inequality for $g$</h3>

The Hoeffding Inequality for any particular hypothesis $h$ bounds the deviation between $E_{in}$ and $E_{out}$ as
$$
\mathbb{P}(|E_{in}(h) - E_{out}(h)| > \epsilon) \leq 2e^{-2\epsilon^2N}
$$


**Small problem**

When bounding the approximation of $E_{out}(g)$ by $E_{in}(g)$, we cannot just plug in $g$ for $h$. This is because $g$ is selected after applying the hypothesis set $\mathcal{H}$ onto the data, so $g$ is cherry-picked based on performance of the hypotheses. 

Instead, we have to use the implication and addition rule of probability. 

**The solution**

If $A \implies B$, then $\mathbb{P}(A) \leq \mathbb{P}(B)$, since event $B$ always occurs whenever $A$ occurs, but may also occur when $A$ does not occur.

Also, $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$ by the addition rule of probability. In fact, we can derive what's called the _Union Bound_ from this rule:

$$
\begin{aligned}
\mathbb{P}(A \cup B)    & =     \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B) \\\
                        & \leq  \mathbb{P}(A) + \mathbb{P}(B)
\end{aligned}
$$

Basically, if $A$ and $B$ are disjoint, then by definition $\mathbb{P}(A \cap B) = 0$, $i.e.$ there is no overlap between $A$ and $B$. This means in general, the union of any two events, disjoint or not, is less than or equal the probability of the disjoint case.

**Translating to our problem**

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

**Discussion on this bound**

We can already see that if the cardinality of the hypothesis space, $|\mathcal{H}| = M$, is infinite, the bound is useless, it is too loose because it considers the worst case that no hypotheses will overlap in their classifications on $\mathcal{D}$. In reality, for any given $\mathcal{D}$, many hypotheses will output the same classifications. Take for instance the perceptron and let's say we have two points, one of which is $+1$ the other $-1$. There are basically an infinite number of $h$'s that would classify these two examples in $\mathcal{D}$ correctly!

Later, we'll see how we can tighten this bound by taking into account these overlapping, or effectively equal, hypotheses.



<h3>Generalization Bound</h3>

From the previous derivation we have
$$
\begin{array}{cl}
& \mathbb{P}(|E_{in}(g) - E_{out}(g)| > \epsilon) \leq 2Me^{-2\epsilon^2N}) \\\ \\\
\implies & \mathbb{P}(|E_{in}(g) - E_{out}(g)| \leq \epsilon) = 1 - \mathbb{P}(|E_{in}(g) - E_{out}(g)| > \epsilon) \\\ \\\
\geq & 1 - 2Me^{-2\epsilon^2N}
\end{array}
$$

$i.e.$ with probability at least $1 - 2Me^{-2\epsilon^2N}$ the following is true
$$
\begin{array}{c}
|E_{in}(g) - E_{out}(g)| \leq \epsilon \equiv E_{out}(g) - E_{in}(g) \leq \epsilon \\\ \\\
\therefore E_{out}(g) \leq E_{in}(g) + \epsilon
\end{array}
$$

Let $\delta = 2Me^{-2\epsilon^2N}$. So with probability at least $1-\delta$
$$
E_{out} \leq E_{in}(g) + \epsilon
$$

But we can express $\epsilon$ in terms of $\delta$

$$
\begin{aligned}
2Me^{-2\epsilon^2N}         & =    \delta \\\ \\\
e^{-2\epsilon^2N}           & =    \frac{\delta}{2M} \\\ \\\
\ln{e^{-2\epsilon^2N}}      & =    \ln{\frac{\delta}{2M}} \\\ \\\
-2\epsilon^2N               & =    \ln{\frac{\delta}{2M}} \\\ \\\
\epsilon^2                  & =    \frac{1}{2N}\ln{\frac{2M}{\delta}} \\\ \\\
\epsilon                    & =    \sqrt{\frac{1}{2N}\ln{\frac{2M}{\delta}}} \\\ \\\
\end{aligned}
$$

$$
\therefore E_{out}(g) \leq E_{in}(g) + \sqrt{\frac{1}{2N}\ln{\frac{2M}{\delta}}}
$$


In fact, we can look at the 3 other inequalities of the Hoeffding bound
$$
P(|E_{in} - E_{out}| > \epsilon) \leq \delta
$$.


The Hoeffding bound directly implies with probability at ***most*** $\delta$:
$$
\begin{aligned}
|E_{in} - E_{out}| > \epsilon   & \equiv    E_{in} - E_{out} > \epsilon \implies E_{out} < E_{in} - \epsilon \quad(1) \\\ \\\
                                & \equiv    E_{out} - E_{in} > \epsilon \implies E_{out} > E_{in} + \epsilon \quad(2) \\\ \\\
\end{aligned}
$$


We already looked at one side of the complement of the Hoeffding bound
$$
P[(|E_{in} - E_{out}| > \epsilon)^C] = P(|E_{in} - E_{out}| \leq \epsilon) \geq \delta
$$

which implies that with probability at ***least*** $1-\delta$:
$$
\begin{aligned}
|E_{in} - E_{out}| \leq \epsilon    & \equiv    E_{in} - E_{out} \leq \epsilon \implies E_{out} \geq E_{in} - \epsilon \quad(3) \\\ \\\
                                    & \equiv    E_{out} - E_{in} \leq \epsilon \implies E_{out} \leq E_{in} + \epsilon \quad(4) \\\ \\\
\end{aligned}
$$


Result $(4)$ is the bound we saw before. Let's go over what these 4 bounds mean.

Results $(1)$ and $(3)$ are what we can think of as our "best case" upper and lower bounds on $E_{out}$, respectively, because they relate $E_{out}$ to the smaller value of $E_{in} - \epsilon$. 

To elaborate, result $(1)$ translates to "we have a ceiling on the probability that $E_{out}$ will be smaller than $E_{in} - \epsilon$, but it is a short ceiling, which means it is far more likely that $E_{out}$ will be closer to being less than or equal to $E_{in} + \epsilon$, $1-\delta$ probable to be more exact.

Flip the logic and we see why $(2)$ and $(4)$ are the "worst case" bounds.

Let's look at result $(3)$ more closely. This result tells us that out of all hypotheses $\mathcal{h} \in \mathcal{H}$, the $g$ selected is likely the best we could do, since there is a fairly high floor, $1-\delta$, on the probability that $E_{in} - \epsilon$ is the lower bound for $E_{out}$. 

Since $g$ was selected as $\underset{h \in \mathcal{H}}{\argmin}(E_{in}(\mathcal{h}))$, every other $h$ will have higher in-sample error, and we have high confidence that out-of-sample error for those hypotheses will also be larger from this bound. $\blacksquare$
