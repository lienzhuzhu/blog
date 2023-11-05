+++
title = "Learning From Data Problem Set 7"
date = "2023-11-04T22:03:50-07:00"
# description = ""

tags = ["notes"]
+++


[PDF of problems](https://work.caltech.edu/homework/hw7.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)



<h3>
1 - 5
</h3

Refer to the output:

```
❯ python3 hw7/validation.py
Q = 3:  K = 10. E_val = 0.300 E_out = 0.420     K = 25: E_val = 0.280 E_out = 0.396
Q = 4:  K = 10. E_val = 0.500 E_out = 0.416     K = 25: E_val = 0.360 E_out = 0.388
Q = 5:  K = 10. E_val = 0.200 E_out = 0.188     K = 25: E_val = 0.200 E_out = 0.284
Q = 6:  K = 10. E_val = 0.000 E_out = 0.084     K = 25: E_val = 0.080 E_out = 0.192
Q = 7:  K = 10. E_val = 0.100 E_out = 0.072     K = 25: E_val = 0.120 E_out = 0.196
```



<h3>
6. [d]
</h3>

We can calculate this analytically. Let $X \sim \textrm{Uniform}(0,1)$ and $Y \sim \textrm{Uniform}(0,1)$. Then $Z=min(X, Y)$ and

$$
\begin{aligned}
P(Z \leq z) &= P(min(X,Y) \leq z) \\\ \\\
    &= 1 - P(X>z \cap Y>z) \\\ \\\
    &= 1 - P(X>z) \cdot P(Y>z) \\\ \\\
    &= 1 - (1-z)^2
\end{aligned}
$$

We differentiate to get the PDF

$$
\begin{aligned}
\frac{d}{dz}(1-(1-z)^2) &= -2(1-z)(-1) \\\ \\\
    &= 2(1-z) \\\ \\\
\end{aligned}
$$

Then find the expectation using the definition of expected value

$$
\begin{aligned}
\mathbb{E}(Z) &= \int_0^1 z \cdot 2(1-z) dz \\\ \\\
    &= 2\int_0^1 z - z^2 dz \\\ \\\
    &= 2\left[\frac{1}{2}z^2 - \frac{1}{3}z^3 \right]\textrm{, } 0 \leq z \leq 1
    &= \frac{1}{3}
\end{aligned}
$$
