# MULTIPROCESSOR SCHEDULING (ADVANCED)

One basic approach is to use a technique known as work stealing [FLR98]. With a work-stealing approach, a (source) queue that is low on jobs will occasionally peek at another (target) queue, to see how it is. If the target queue is (notably) more full than the source queue, the source will "steal" from the target to help balance load.

Of course, there is a natural tension in such an approach. If you look around at other queues too often, you will suffer from high overhead and trouble scaling, which was the entire purpose of implementing the multiple queue scheduling in the first place! If, on the other hand, you don't look at other queues very often, you are in danger of suffering from severe load imbalances. Finding the right threshold remains, is common in system policy design, a black art.

# 10.6 Multiprocessor Schedulers

Interestingly, in the Linux community, no common solution has proposed building a multiprocessor scheduler. Over time, different schedulers arose: the O(1) scheduler, the Completely Fair Scheduler (CFS), and the BF Scheduler (BFS). See Meehan's dissertation for an excellent overview of the strengths and weaknesses of schedulers [M11]; here we summarize a few of basics.

Both O(1) and CFS use multiple queues, BFS uses a single queue, showing that both approaches can be successful. Of course, there are many other methods which separate these schedulers. For example, the O(1) scheduler is a priority-based scheduler (similar to the MLFQ discussed before), changing a process priority over time and scheduling with higher priority in order to meet various objectives; interactivity is a particular focus. BFS, in contrast, is a deterministic proportional-share approach (like Stride scheduling, as discussed earlier). The only single-queue approach among the three, is proportional-share, but based on a more complicated scheme known as Earliest Linux Virtual Deadline First (EVDF) [SA96]. Read more about these modern algorithms on your own; you should be able to understand how they work now!

# 10.7 Summary

We have seen various approaches to multiprocessor scheduling. The single-queue approach (SQMS) is rather straightforward to build and balance well but inherently difficulty with scaling to many processors and cache affinity. The multi-queue approach (MQMS) scales better and handles cache affinity well, but has trouble with load imbalance. Whichever approach you take, there is no simple answer: building a general purpose scheduler remains a daunting task, as small code changes can lead to large behavioral differences. Only undertake an exercise if you know exactly what you are doing, or, at least, are getting a large amount of money to do so.

> Look up what BF stands for on your own; beware, it is not for the faint of heart.

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG