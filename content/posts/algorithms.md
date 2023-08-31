+++
title = "Hack Pack"
date = "2023-08-29T16:04:59-07:00"
# description = "Notes on DSA for competitive programming"

tags = ["engineering"]
draft = true
+++


### Union-Find / Disjoint Set

- Union by Rank modifies union() to optimize find() and union() by balancing the tree.
- Path Compression modifies find() to have a recursive call, essentially sharing the burden of updating root pointers between both find() and union().
