# SCHEDULING: PROPORTIONAL SHARE

| A | B | C | D | A | B | C | D | A | B | A | B |
|---|---|---|---|---|---|---|---|---|---|---||}{
| 0 | | 50 | | 100 | | 150 | | 200 | | 250 |

Figure 9.4: CFS Simple Example

# Basic Operation

Whereas most schedulers are based around the concept of a fixed time slice, CFS operates a differently. Its goal is simple: to fairly divide the CPU among all competing processes. It does so through a simple counting-based technique as *virtual runtime*.

As each process runs, it accumulates *runtime*. In the most basic case, each process's *runtime* increases at the same rate, in proportion with physical (real) time. When a scheduling decision occurs, CFS will pick the process with the *lowest runtime* to run next.

This raises a question: how does the scheduler know to stop the currently running process, and run the next? The tension here is: if CFS switches too often, fairness is increased, CFS will ensure that each process receives its share of CPU even over minimum time windows, but at the cost of performance (too many context switching); CFS switches less often, performance is increased (reduced context switching), but at the cost of interactivity.

CFS manages this through various control parameters. The first is *sched_latency*. CFS uses this value to determine how long one process should run before considering a switch (effectively determining its time slice but in a dynamic fashion). A typical *sched_latency* value is 48 (milliseconds); CFS divides this value by the *(n) of processes running on the CPU to determine the time slice for a process, and ensures that over this period of time, CFS will be completely fair.

For example, if *n=4* processes, CFS divides the value of *sched_latency* by *n* to arrive at a per-process slice of 12 ms. CFS then schedules the first and runs it for 12 ms of (virtual) runtime, and then checks to see if there is a job with lower *runtime* to run next. In this case, it would switch to one of the other three and so forth. Figure 9.4 shows an example where the four jobs (A, B, C, D) run for two time slices in this; two of them (C, D) complete, just two remaining, which each run for 24 ms in round-robin fashion.

But if there are “too many” processes running? Wouldn't that lead to too small of a time slice, and thus many context switches? Good question! And the answer is yes.

To address this issue, CFS adds another parameter, *min_granularity*, which is usually set to a value like 6 ms. CFS will never set the time slice

OPERATING
SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG