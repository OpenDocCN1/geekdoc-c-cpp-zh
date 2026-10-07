# SCHEDULING:
THE MULTI-LEVEL FEEDBACK QUEUE

91

![](bbox=[0.163, 0.141, 0.786, 0.329])

Figure 8.6: Without (Left) and With (Right) Gaming Tolerance

# 8.3 Attempt#2: The Priority Boost

Let's try to change the rules and see if we can avoid the problem of starvation. What could we do in order to guarantee that CPU-bound jobs will make some progress (even if it is not much?)

The simple idea here is to periodically boost the priority of all the jobs in system. There are many ways to achieve this, but let's do something simple: move them to the topmost queue; hence, a new rule:

+   Rule 5: After some time period S, move all the jobs in the system to the topmost queue.

Our rule solves two problems at once. First, processes are guaranteed not to starve: by sitting in the queue, a job will serve the CPU with other high-priority jobs in a round-robin fashion, and thus eventually receive service. Second, if a CPU-bound job becomes interactive, the scheduler treats it properly once it has received the priority boost.

Let's see an example. In this scenario, we show the behavior of a long-running job when competing for the CPU with two short-running interactive jobs. Two graphs are shown in Figure 8.5 (page 90). On the left, there is no priority boost, and thus the long-running job starved once the two short jobs arrive; on the right, there is a priority boost every 50 ms (which is likely too much of a value, but here for the example), and we at least guarantee that the long-running job will make some progress, boosted to the highest priority every 50 ms and thus running periodically.

Of course, the addition of the time period S leads to the obvious question: what should S be set to? John Ousterhout, a well-regarded researcher [011], used to call such values in systems woo-doo contestants, because they seemed to require some form of black magic to get them correctly. Unfortunately, S has that flaw. If it is too high, long-running jobs could starve; too low, and interactive jobs may not get a proper share of the CPU.

© 2008–19, ARPACI-DUSSE

THREE
ASY
PIECES

* Asterimi*