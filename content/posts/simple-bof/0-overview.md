+++
title = "Simple Buffer Overflow Attacks 0 - Series Introduction"
date = "2023-05-11T23:43:03-05:00"
description = "Introduction to series on buffer overflow attacks with various combinations of protections."

tags = ["system","software","security","gdb"]
+++


In this series, we will explore the stack-based buffer overflow attack with 4 combinations of protections.

This series focuses on stack-based buffer overflow. Learning heap-based buffer overflow is a TODO.

The [first] post assumes no protections are enabled. Then we will think about how to exploit systems that have either Address Space Layout Randomization (ASLR) or No-Execute (NX) protections as well as a system that has both protections enabled.


# Process Memory Layout

One of the abstractions that the operating system provides to each process is the virtualization of memory, which makes it appear as if each process has full access to the total memory space, and has the same range of memory addresses available for use data storage.

The following diagram from Randall Bryant adn David O'Hallaron's book _Computer Systems: A Programmer's Perspective_ displays the address space layout.

!["Computer Systems: A Programmer's Perspective by Randall Bryant and David O'Hallaron"](/blog/images/simple-bof/memory.png)


# Closer look at the stack

The section called the stack grows downward at run-time as functions are called. If we look closer at the stack, we'll notice the return address bytes are pushed onto the stack so the CPU knows what instruction to return to after running a function.

!["https://hackmag.com/security/stack-overflow/"](/blog/images/simple-bof/stack.png)

We will take control of the return address by overwriting the value by overflowing a local buffer variable in the function body.