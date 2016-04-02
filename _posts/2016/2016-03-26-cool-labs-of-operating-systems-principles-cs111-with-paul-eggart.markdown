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
 it turns out to be the best CS course I've ever taken (except for its exams. I almost got full marks for every lab, but it seems I did not do will in the final because I accidentally lost half of my open notes before the exam. Time to test my memory).<!--more-->

   We have in total 6 labs (4 main lab, 2 mini lab). I summarized the main task of the labs in one sentence each.

   * Lab1 (part a, b, c): Implement a "simpsh" command which creates arbitrary directed graphs of processes connected via pipes, along with a performance comparison with other shell-like programs.
   * Lab2: Write an in-memory block device driver as a Linux kernel module, copping with some interesting synchronization issues invoked by read/write lock.
   * Lab3: Writing a simple in-memory file system for Linux.
   * Lab4: Practice and gauge parallelism and synchronization issues on complicated data structures.  
   * Mini Lab1: Implement your own fork, waitpid system call.
   * Mini Lab2: Implement your own process scheduling algorithms and compare their performance.

The First lab is newly designed by Prof.Eggart and was comparatively open (because there had been no standard answer code yet). Lab 2 and 3 are classic labs for CS 111 with a [repository in my Github](https://github.com/milesyao/CS111-Labs) (I finished mine independently). Lab 4 is newly designed by Prof.Kampe, who will be teaching CS 111 during Spring quarter.

Here comes Lab1 and Lab2.

#### [Lab 1. Simpleton shell](/assets/others/lab1.html)
* The thing I learnt through this lab is the usage and best practice of [Getopt](http://www.gnu.org/software/libc/manual/html_node/Getopt.html)
  The example shown in official tutorial is not sufficient. As _Getopt_'s judgement unit is by default separated by spaces, what if we want to catch "```--command cat 1 2 3```"together? In that case _optind_ variable is our best friend. We used _k_ to denode our judgement margin.   
  ```for(;optind<argc && !(*argv[optind] == '-' && *(argv[optind]+1) == '-'); optind++) k++;
  if(k>=2) fprintf(stderr, "Warnning: --wronly: Too many arguments. Use the first one.\n");
  if(k==0) {
      fprintf(stderr, "--wronly: Require an argument\n");
      break;
  }
  if(verbose_flag) {
      printf("--wronly %s\n", argv[optind-1]);
  }
  ```

  Another thing to note is using macro definition to make in-line Getopt options cleaner. For example, define:
  ```
  #define RDONLY 'a'
  #define WRONLY 'b'
  #define COMMAND 'c'
  #define CREAT 'd'
  ```
  at the top and then inside Getopt:
  ```
  switch (c)
  {            
    case 0:
      break;
    case WRONLY:
      ...
    case RDONLY:
      ...
    case COMMAND:
      ...
    case CREAT:
      ...
  ```
  Rather than:
  ```
  switch (c)
  {            
    case 0:
      break;
    case 'a':
      ...
    case 'b':
      ...
    case 'c':
      ...
    case 'd':
      ...
  ```
  which is difficult to read for other code reviewers and for yourself, I just recalled [JAVA Bean](https://en.wikipedia.org/wiki/JavaBeans) seems to have a similar taste as this practice.

* How to use GNU C library to create new process(fork) and restore them using waitpid function call.

My main reference is [Tuan's discussion note](/assets/files/tuanlab1.txt).

* Besides these, as this lab requires us to implement a command which can create arbitrary directed graphs of processes connected via pipes. This requires additional data structure and program design.

I used C struct and hashtable to store process meta data and file descriptor cast. Please refer to comments in the source code.

* Finally in project 1c, we are required to gauge CPU/Wall time using getrusage. Also we should compare the result with bash and execline and justify the pros and cons using our simpleton shell.

Actually this is the worst part of project 1. The lab description is vague and execline is hard to use. Once I add one more space in calling execline, which cost me 2 hours to debug. Screw it!

### [Lab2.RamDisk](/assets/files/lab2.webarchive)
The most important part of this lab is to understand how read/write lock work together. Most APIs have been explained by course website. But one point that was once confusing to lots of students including me is the differences between tickets list and pid list. Ticket list are tickets to be assigned. Pid list are processes currently holding the lock.

As new term has started, I don't know if I have time to continue this series. Will see :)
