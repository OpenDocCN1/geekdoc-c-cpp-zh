
# SCHEDULING: PROPORTIONAL SHARE

priority by assigning it a nice value of -5; B, because we hate it [it] just has the default priority (nice value equal to 0). This means $weight_A$ (from the ta-) is 3121, whereas $weight_B$ is 1024. If you then compute the time slice of each job, you'll find that A's time slice is $2/3$ of sched_latency (hence, 36 ms), and B's $1/2$ (hence, 12 ms).

In addition to generalizing the time slice calculation, the CFS runtime must also be adapted. Here is the new formula, which takes the actual run time that process $i$ has accrued ($runtime$) and scales inversely by the weight of process $i$. In our running example, A's runtime will accumulate one-third of B's.

```
$runtime = runtime, + \frac{weight_0}{weight_i} \cdot runtime\quad (9.2)$
```

One smart aspect of the construction of the table of weights is that the table preserves CPU proportionality ratios when the difference in nice values is constant. For example, if A instead had a nice value of 5 (not -5), and process B had a nice value of 10 (not 0), CFS would schedule them exactly in the same manner as before. Run that yourself to see.

# Using Red-Black Trees

One major focus of CFS is efficiency, as stated above. For a scheduler, there are many facets of efficiency, but one of them is as simple as this: when the scheduler has to find the next job to run, it should do so as quickly as possible. Simple data structures like lists don't scale: modern systems are comprised of thousands of processes, and searching through a long list every few milliseconds is wasteful.

CFS addresses this by using balanced trees; in contrast to simple binary tree (which can generate list-like performance under worst-case), balanced trees do a little extra work to maintain low depths, and ensure that operations are logarithmic (and not linear) in time. CFS does not keep all process in this structure; rather, only runnable processes are kept. If a process goes to sleep (say, waiting on I/O to complete, or for a network packet to arrive), it is removed from the tree and kept elsewhere.

Let's look at an example to make this clear. Assume there are ten jobs, and they have the following values of runtime: 1, 5, 9, 10, 14, 17, 21, 22, 24. If we keep these in an ordered list, finding the next job to run would be simple: just insert the first element. However, placing job back into the list (in order), would have to scan the list, looking for the right spot to insert it, an $O(n)$ operation. Search is also quite inefficient, taking linear time on average.

Keeping the same values in a red-black tree makes most operations more efficient, as depicted in Figure 9.5. Processes are ordered in the tree by vruntime, and most operations (such as insertion and deletion) are logarithmic in time, i.e., $O(\log n)$. When $n$ is in the thousands, logarithmic is noticeably more efficient than linear.

# Dealing With I/O And Sleeping Processes

One problem with picking the lowest $vruntime$ to run arises with processes that have to sleep for a long period of time. Imagine two processes, A and B, one of which (A) runs continuously, and the other (B) which has to sleep for a long period of time (say, 10 seconds). When B wakes up, its $vruntime$ will be low and thus (if we are not careful), B will now monopolize the CPU for the next 10 seconds until it catches up, effectively starving A.

CFS handles this case by altering the $vruntime$ of a job when it wakes up. Specifically, CFS sets the $vruntime$ of that job to the minimum value found in the tree (remember, the tree only contains running jobs). In this way, CFS avoids starvation, but not without a cost: jobs that sleep for short periods of time frequently do not get their fair share of the CPU.

# Other CFS Features

CFS has many other features to discuss at this point in the book. It includes numerous heuristics to improve cache performance, strategies for handling multiple CPUs effectively (as discussed later in the book), can schedule large groups of processes effectively (instead of treating each process as an independent entity), and many other interesting features. Read recent research, starting with to learn more.

# 9.8 Summary

We have introduced the concept of proportional-share scheduling and briefly discussed three approaches: lottery scheduling, stride scheduling, and the Completely Fair Scheduler (CFS) of Linux. Lottery uses randomness in a clever way to achieve proportional share; stride, the only “real” scheduler does so deterministically, with bit like weighted round-robin slices, but built to scale and perform well under load; to our knowledge, it is the most widely used fair-share scheduler in existence today.

No scheduler is perfect, and fair-share schedulers have their fair share of problems. One issue is that these approaches do not particularly mesh with I/O; as mentioned above, jobs that perform I/O occasionally may not get their share of CPU. Another issue is that they leave the hard problem of ticket or priority assignment, i.e., to what value set your tickets to your text editor? Other general-purpose schedulers (such as) are used. In the case discussed here, simple lists found in earlier schedulers simply do not work well on modern systems. A better structure was needed, and CFS provided one by an excellent implementation of a red-black tree. More generally, picking a data structure for a system you are building, carefully consider its access patterns and its frequency of use; by understanding these, you will be able to implement the right structure for the task at hand.

# SCHEDULING: PROPORTIONAL SHARE

> TIP: USE EFFICIENT DATA STRUCTURES WHEN APPROPRIATE
In many cases, a list will do. In many cases, it will not. Knowing which data structure to use is a hallmark of good engineering.
