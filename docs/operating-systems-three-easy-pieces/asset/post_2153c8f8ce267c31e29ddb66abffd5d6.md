
# SCHEDULING: PROPORTIONAL SHARE

## 9.5 How To Assign Tickets?

One problem we have not addressed with lottery scheduling is: how to assign tickets to jobs? This problem is a tough one, because course how the system behaves is strongly dependent on how tickets are allocated. One approach is to assume that the users know best; in such a case, each user is handed some number of tickets, and a user can allocate tickets to any jobs they run as desired. However, this solution is a nonsolution: it really doesn't tell you what to do. Thus, given a set of jobs, the 'ticket-assignment problem' remains open.

## 9.6 Why Not Deterministic?

We might be wondering; why use randomness at all? As we saw above, randomness gets us a simple (and approximately correct) scheduler, it occasionally will not deliver the exact proportions, especially over short times. For these reasons, Walspurger invented scheduling, a deterministic fair-share scheduler [W95].

Stride scheduling is straightforward. Each job in the system has a stride, which is in proportion to the number of tickets it has. In our example above, with jobs A, B, and C with 100, 50, and 250 tickets, respectively, we can compute the stride of each by dividing some number by the number of tickets each process has been assigned. For example, if we divide 1000 by each of those tickets, we obtain the following stride values for A, B, and C: 100, 200, and 40. We call the stride of each process; every time a process runs, we will increment a counter for it (its pass value) by its stride to track its global progress.

The scheduler uses the stride and pass to determine which process should run next. The basic idea is simple: at any given time, pick the process to run that has the lowest pass value so far; when a process runs, increment its counter by its stride. A pseudocode implementation by Walspurger [W95]:

```
curr = remove_min(queue); // pick client with min pass
schedule(curr);               // run for quantum
curr->pass += curr->stride; // update pass using stride
insert(queue, curr);       // return to queue
```

In our example, with three processes (A, B, and C), with stride values of 100, 200, and 40, and with pass values initially at 0. Thus, at first, any of the processes might run, as their pass values are equally low. We assume pick (arbitrarily); any of the processes with equal low pass values can be chosen). A runs; when finished with the time slice, we update its pass value to 0. Then we run B, whose pass value is set to 200. Finally, we run C, whose pass value is incremented to 40. At this point, the algorithm will pick the lowest pass value, which is C's, and run it, updating its pass value to 80 (C's stride, as you recall). Then C will run again (still the lowest pass value), raising its pass to 120. A will run now, updating its pass to 200 (now equal to B's). Then C will run twice, updating its pass 160 to 200. At this point, all pass values are equal, and the process will run, ad infinitum. Figure 9.3 traces the behavior of the scheduler over time.

As we can see from the figure, C runs five times, A and B once, exactly in proportion to their ticket values (25, 100, and 50). Lottery scheduling achieves the proportionally over time; stride scheduling them exactly right at the end of each scheduling cycle.

So you might be wondering: why lottery scheduling at all? Lottery scheduling has one nice property that stride scheduling does not: no global state. Imagine a new job enters the middle of our stride scheduling example above; what would its pass value be? If it is set to 07? If so, we will monopolize the CPU. With lottery scheduling, there is no global state per process; we simply add a new process with whatever tickets it has, update the single global variable to track how many tickets we have, and go from there. In this way, lottery makes it much easier to incorporate new processes in a sensible manner.

## 9.7 The Completely Fair Scheduler (CFS)

Despite early experiments in fair-scheduling, the Linux Linux achieves similar goals in an alternate manner. The scheduler, entitled the Completely Fair Scheduler (or CFS) [J09], implements fair-sharing, but does so in a highly efficient and scalable manner.

To achieve its efficiency, CFS aims to spend little time making scheduling decisions, both through its inherent design and the clever use of data structures well-suited to the task. Recent studies have shown that scheduler efficiency is surprisingly important; specifically, in a study of Google datacenters, Kanev et al. show that even aggressive optimization, scheduling uses up about 5% of overall datacenter CPU time. Reducing overhead as much as possible is thus a key goal in modern scheduler architecture.

| A | B | C | D | A | B | C | D | A | B | A | B |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | | 50 | | 100 | | 150 | | 200 | | 250 |

Figure 9.4: CFS Simple Example

### Basic Operation

Whereas most schedulers are based around the concept of a fixed time slice, CFS operates a differently. Its goal is simple: to fairly divide the CPU among all competing processes. It does so through a simple counting-based technique as *virtual runtime*.

As each process runs, it accumulates *runtime*. In the most basic case, each process's *runtime* increases at the same rate, in proportion with physical (real) time. When a scheduling decision occurs, CFS will pick the process with the *lowest runtime* to run next.

This raises a question: how does the scheduler know to stop the currently running process, and run the next? The tension here is: if CFS switches too often, fairness is increased, CFS will ensure that each process receives its share of CPU even over minimum time windows, but at the cost of performance (too many context switching); CFS switches less often, performance is increased (reduced context switching), but at the cost of interactivity.

CFS manages this through various control parameters. The first is *sched_latency*. CFS uses this value to determine how long one process should run before considering a switch (effectively determining its time slice but in a dynamic fashion). A typical *sched_latency* value is 48 (milliseconds); CFS divides this value by the *(n) of processes running on the CPU to determine the time slice for a process, and ensures that over this period, 

| Pass(A) | Pass(B) | Pass(C) | Who Runs? |
|---|---|---|---|
| (stride=100) | (stride=200) | (stride=40) | |
| 0 | 0 | 0 | A |
| 100 | 0 | 0 | B |
| 100 | 200 | 0 | C |
| 100 | 200 | 40 | C |
| 100 | 200 | 80 | A |
| 100 | 200 | 120 | C |
| 200 | 200 | 160 | C |
| 200 | 200 | 200 | ... |

Figure 9.3: Stride Scheduling: A Trace

OPERATING SYSTEMS [Version 1.01]
WWW.OSTEP.ORG

# SCHEDULING: PROPORTIONAL SHARE

### Weight (Niceness)

CFS also controls over priority, enabling users or administrators to give some higher share of the CPU. This does not with tickets, but through a classic mechanism known as the level of process. The nice parameter can be anything from -10 to +19, with a default of 0. Positive nice values lower priority and negative values imply higher priority; when you're too nice, you just don't get as much attention. CFS maps the value of each process to a weight, as shown here:

```
static const int prio_to_weight[40] = {
    /* -20 */ 88761, 71755, 56483, 46273, 36291,
    /* -15 */ 29154, 23254, 18705, 14949, 11916,
    /* -10 */ 9548, 7620, 6100, 4904, 3906,
    /* -5 */ 3121, 2501, 1991, 1586, 1277,
    /* 0 */ 1024, 820, 655, 526, 423,
    /* 5 */ 335, 272, 215, 172, 137,
    /* 10 */ 110, 87, 70, 56, 45,
    /* 15 */ 36, 29, 23, 15,
};
```

These weights allow us to compute the time slice of each process (as we did before), but now accounting for their priority differences. The formula used to do so is:

```
time_slice_k = \frac{\sum_{i=0}^{n-1} weight_i}{weight_k} \cdot sched_latency   (9.1)
```

Let's do an example to see how this works. Assume there are two jobs, A and B, because because it's our most precious job, is given a higher pri-
