+++
title = "Learning From Data Problem Set 8"
date = "2023-11-10T17:17:05-08:00"
# description = ""

draft = true
tags = ["notes", "ml"]
+++

[PDF of problems](https://work.caltech.edu/homework/hw8.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)


<h3>
1. [d]
</h3>

With the primal problem solves for the weights and the bias term directly, which makes $d+1$ variables of interest.


<h3>
2. [a]
</h3>

```
❯ python3 hw8/poly_svm.py
0 versus all  E_in: 0.11905  E_out: 0.12855
1 versus all  E_in: 0.01426  E_out: 0.02242
2 versus all  E_in: 0.10026  E_out: 0.09865
3 versus all  E_in: 0.09025  E_out: 0.08271
4 versus all  E_in: 0.08943  E_out: 0.09965
5 versus all  E_in: 0.07626  E_out: 0.07972
6 versus all  E_in: 0.09107  E_out: 0.08470
7 versus all  E_in: 0.08847  E_out: 0.07324
8 versus all  E_in: 0.07434  E_out: 0.08271
9 versus all  E_in: 0.08833  E_out: 0.08819
```


<h3>
3. [a]
</h3>

```
❯ python3 hw8/poly_svm.py
0 versus all  E_in: 0.11905  E_out: 0.12855
1 versus all  E_in: 0.01426  E_out: 0.02242
2 versus all  E_in: 0.10026  E_out: 0.09865
3 versus all  E_in: 0.09025  E_out: 0.08271
4 versus all  E_in: 0.08943  E_out: 0.09965
5 versus all  E_in: 0.07626  E_out: 0.07972
6 versus all  E_in: 0.09107  E_out: 0.08470
7 versus all  E_in: 0.08847  E_out: 0.07324
8 versus all  E_in: 0.07434  E_out: 0.08271
9 versus all  E_in: 0.08833  E_out: 0.08819
```


<h3>
4. [c]
</h3>

```
❯ python3 hw8/poly_svm.py
0 versus all  E_in: 0.11905  E_out: 0.12855  SVs: 2279
1 versus all  E_in: 0.01426  E_out: 0.02242  SVs: 400
2 versus all  E_in: 0.10026  E_out: 0.09865  SVs: 1488
3 versus all  E_in: 0.09025  E_out: 0.08271  SVs: 1351
4 versus all  E_in: 0.08943  E_out: 0.09965  SVs: 1325
5 versus all  E_in: 0.07626  E_out: 0.07972  SVs: 1131
6 versus all  E_in: 0.09107  E_out: 0.08470  SVs: 1341
7 versus all  E_in: 0.08847  E_out: 0.07324  SVs: 1310
8 versus all  E_in: 0.07434  E_out: 0.08271  SVs: 1121
9 versus all  E_in: 0.08833  E_out: 0.08819  SVs: 1306
```

$$
2279 - 400 = 1879
$$
