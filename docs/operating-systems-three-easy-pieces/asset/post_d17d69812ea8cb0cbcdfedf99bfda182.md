
# SCHEDULING:
THE MULTI-LEVEL FEEDBACK QUEUE

90

Q2

Q2

Q1

Q1

Q0

Q0

![](img/133d518e3f69f4caaead32c569ae6c49_127_0.png)

Figure 8.5: Without (Left) and With (Right) Priority Boost

First, there is the problem of starvation: if there are "many" interactive jobs in the system, they will combine to consume all CPU time, and thus long-running jobs will never receive any CPU time (they starve). We'd like to make progress on these jobs in this scenario.

Second, a smart user could rewrite their program to game the scheduler by doing something sneaky to trigger the scheduler. Gaming the scheduler generally refers to the idea of giving you more than your share of the resource. The algorithm we have described is susceptible to the following attack: before the time slice is over, issue an I/O operation (to some file you don't care about) and thus relinquish the CPU; doing so allows you to remain in the same queue, and gain a higher percentage of CPU time. When done right (e.g., by running for 99% of a time slice relinquishing the CPU), a job could nearly monopolize the CPU.

Finally, a program may change its behavior over time, what was CPU-bound may transition to a phase of interactivity. With our current approach, such a job would be out of luck and not treated like the other interactive jobs in the system.

> TIP: SCHEDULING MUST BE SECURE FROM ATTACK

You might think that a scheduling policy, whether the OS itself (as discussed here), or in a broader context (e.g., in a distributed system's I/O request handling [Y+18]), is not a security concern, but in increasingly many cases, it is exactly that. Consider the modern datacenter, in which users from around the world share CPUs, memories, networks, and storage; without in policy design and enforcement, a single user may be able to adversely harm others and gain advantage for itself. Thus, scheduling policy forms an important part of the security of a system, and should be carefully constructed.

OPERATING
SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

# SCHEDULING:
THE MULTI-LEVEL FEEDBACK QUEUE

91

![](img/133d518e3f69f4caaead32c569ae6c49_128_0.png)

Figure 8.6: Without (Left) and With (Right) Gaming Tolerance

# 8.3 Attempt#2: The Priority Boost

Let's try to change the rules and see if we can avoid the problem of starvation. What could we do in order to guarantee that CPU-bound jobs will make some progress (even if it is not much?)

The simple idea here is to periodically boost the priority of all the jobs in system. There are many ways to achieve this, but let's do something simple: move them to the topmost queue; hence, a new rule:

- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.

Our rule solves two problems at once. First, processes are guaranteed not to starve: by sitting in the queue, a job will serve the CPU with other high-priority jobs in a round-robin fashion, and thus eventually receive service. Second, if a CPU-bound job becomes interactive, the scheduler treats it properly once it has received the priority boost.

Let's see an example. In this scenario, we show the behavior of a long-running job when competing for the CPU with two short-running interactive jobs. Two graphs are shown in Figure 8.5 (page 90). On the left, there is no priority boost, and thus the long-running job starved once the two short jobs arrive; on the right, there is a priority boost every 50 ms (which is likely too much of a value, but here for the example), and we at least guarantee that the long-running job will make some progress, boosted to the highest priority every 50 ms and thus running periodically.

Of course, the addition of the time period S leads to the obvious question: what should S be set to? John Ousterhout, a well-regarded researcher [011], used to call such values in systems woo-doo contestants, because they seemed to require some form of black magic to get them correctly. Unfortunately, S has that flaw. If it is too high, long-running jobs could starve; too low, and interactive jobs may not get a proper share of the CPU.

© 2008–19, ARPAC-DUSSE

THREE
ASY
PIECES

* Asterimi*

# SCHEDULING:
THE MULTI-LEVEL FEEDBACK QUEUE

![](img/133d518e3f69f4caaead32c569ae6c49_129_0.png)

Figure 8.7: Lower Priority, Longer Quanta

# 8.4 Attempt#3: Better Accounting

We now have one more problem to solve: how to prevent gaming the scheduler? The real culprit is, as you have guessed, the solution is to perform better accounting of MLFQ. The scheduler should keep track of how much of time slice is used at each level, and demote it to the next queue. We then use the following:

- Rule 4: If a job uses its allotment, it is demoted to the next (lower) queue.

Let's look at an example. Figure 8.6 (page 91) shows what happens when a workload tries to game the scheduler (on the left, there is no priority boost, and on the right, there is a priority boost every 50 ms (which is likely too much of a value, but here for the example)). The high-priority queues are given short time slices; they are comprised of interactive jobs, after all, and thus it makes sense. The low-priority queues, in contrast, contain long-running jobs thatare CPU-bound; hence, longer time slices work well (hundred of ms).

# 8.5 Tuning MLFQ and Other Issues

Other issues arise with MLFQ. One question is how to parameterize the scheduler. For example, how many queues should there be? How big the time slice be? How often to boost priority of a job? There are no easy answers to these questions, and thus only experience with MLFQ will lead to a satisfactory balance.

> TIP: SCHEDULING MUST BE SECURE FROM FROM ATTACK

Avoiding voodoo constants is a good idea. Unfortunately, as in the example above, it is often difficult. This is brought to you by our old OS professor, John Ousterhout, and here we call it Ousterhout's Law.

For example, MLFQ queues allow for varying time-slice length across queues. The Solaris MLFQ implementation — The Time-Sharing class, or TS — is particularly easy to configure; it provides a set of tables det how the priority of a job is processed out its lifetime, how long each time slice is, and how often to boost priority of a job [AD00]; an administrator can muck with this table in order to make the scheduler behave in different ways. Default values for are 60 queues, with slowly increasing time-slice lengths from 20 milliseconds (highest priority) to a few hundred milliseconds (lowest), and priorities boosted around 1 second or so.

Other MLFQ consider don't use a table or the rules defined in this chapter; they adjust priorities using mathematical formulas. For example, the FreeBSD scheduler (version 4.3) uses a formula to calculate the current priority of a job, basing on how much CPU has, usage is decayed over time, hiding the desired priority boost in a different manner than does here. See Epema's paper for an excellent overview of decay-usage algorithms and their properties [E95].
