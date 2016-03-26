---
layout: "post"
title: "Cool labs of Operating Systems Principles (CS111) with Paul Eggert"
date: "2016-03-26 09:30"
tags:
  - UCLA
  - CS 111
  - Operating Systems
---
In the following 3 posts I will summarize some of my codes from last quarter's
 CS 111 (Operating Systems Principles) with Prof.Eggert.

 At the beginning of last quarter, I was told [CS 111 of Winter 2016](http://web.cs.ucla.edu/classes/winter16/cs111/)
 would still be a tough one with extensive coding assignments. Worried a little at first,
 it turns out to be the best CS course I've ever taken (except for its exams. I almost got
   full marks for every lab, but it seems I did not do will in the final because I accidentally lost half of my open notes before the exam. Time to test my memory).<!--more-->

   We have in total 6 labs (4 main lab, 2 mini lab). I summarized the main task of the labs in one sentence each.

   * Lab1 (part a, b, c): Implement a "simpsh" command which creates arbitrary directed graphs of processes connected via pipes, along with a performance comparison with other shell-like programs.
   * Lab2: Write an in-memory block device driver as a Linux kernel module, copping with some interesting synchronization issues invoked by read/write lock.
   * Lab3: Writing a simple in-memory file system for Linux.
   * Lab4: Practice and gauge parallelism and synchronization issues on complicated data structures.  
   * Mini Lab1: Implement your own fork, waitpid system call.
   * Mini Lab2: Implement your own process scheduling algorithms and compare their performance.

The First lab is newly designed by Prof.Eggart and was comparatively open (because there had been no standard answer code yet). Lab 2 and 3 are classic labs for CS 111 with existing repositories in Github (I finished mine independently). Lab 4 is newly designed by Prof.Kampe, who will be teaching CS 111 during Spring quarter.

Here comes Lab1 and Lab2.

#### [Lab 1. Simpleton shell](/assets/others/lab1.html)
