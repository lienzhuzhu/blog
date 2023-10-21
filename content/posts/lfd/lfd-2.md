+++
title = "Learning From Data Problem Set 2"
date = "2023-10-20T18:25:47-07:00"
# description = ""

tags = ["notes"]
+++


Below are my solutions to the second problem set from the self-paced version of the CS 156 course at Caltech. [PDF of problems](https://https://work.caltech.edu/homework/hw2.pdf)

[Code Repository](https://github.com/lienzhuzhu/lfd)


Refer to the code repository above for problems 1 and 2. Usage: `python3 coin.py`.

**1. [b]**

I get around 0.03 - 0.04 for the average value of $\nu_{min}$ so the correct answer is pretty close to being 0.1 but alas it is still correct to say 0.01.


**2. [d]**

The graphs show us that the $c_{min}$ coin is not bounded by the Hoeffding bound as we would expect. This makes sense because the Hoeffding inequality only applies to situations where we decide on a strategy before working on the data. In the learning problem, we pick $g$ based on the performance of many $h$'s on the dataset.


Here's a short elaboration on the Hoeffding bound:


