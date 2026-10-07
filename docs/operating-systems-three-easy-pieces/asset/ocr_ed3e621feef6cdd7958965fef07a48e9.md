# SCHEDULING: PROPORTIONAL SHARE

TIP: USE RANDOMNESS

One of the most beautiful aspects of lottery scheduling is its use of **randomness**. When you have to make a decision, using such a randomized approach is often a robust and simple way of doing so.

Random approaches have at least three advantages over more traditional decisions. First, random often avoids strange corner-behavior that a more traditional algorithm may have trouble handling. For example, consider the LRU replacement policy (studied in more detail in a chapter on virtual memory); while often a replacement algorithm, LRU attains worst-case performance for some cyclic-sequential workload. Random, on the other, has no worst case.

Second, random is lightweight, requiring little to track alternatives. In a traditional fair-share scheduling algorithm, tracking how much CPU each process requires per-process accounting, which must be updated after running each process. Doing so randomly necessitates only the minimal of per-process state (e.g., the number of tickets each has).

Finally, random can be quite fast. As long as generating a random number is quick, making the decision is also, and thus random can be used in a number of places where speed is required. The faster the need, the more random tends towards pseudo.

a winning ticket, which is a number from 0 to 99¹. Assuming A holds tickets 0 through 74 and B 25 through 99, the winning ticket simply determines whether A or B runs. The scheduler loads the state of that winning process and runs it.

Here is an example output of a lottery scheduler's winning tickets:

63 85 70 39 76 17 29 41 36 10 99 68 83 62 43 00 49

Here is the resulting schedule:

A A A A A A A A A A
B B B B B B B B B

As you can see from the example, the use of randomness in lottery scheduling leads to a probabilistic correctness in the desired proportion, but no guarantee. In our example, B only gets 4 out of 20 time slices (20%), instead of the desired 25% allocation. However, the longer these two jobs compete, the more likely they are to achieve the desired percentages.

> ¹Computer Scientists always counting at 0. It is also to add to non-computer-types that famous people have felt obliged to write about why we do this way [D82].

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG