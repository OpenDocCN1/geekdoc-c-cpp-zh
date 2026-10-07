# SCHEDULING: PROPORTIONAL SHARE

ority by assigning it a nice value of -5; B, because we hate it just has the default priority (nice value equal to 0). This means $weight_A$ (from the ta- is 3121, whereas $weight_B$ is 1024. If you then compute the time slice of each job, you'll find that A's time slice is $rac{2}{3}$ of sched_latency (hence, 36 ms), and B's $rac{1}{2}$ (hence, 12 ms).

In addition to generalizing the time slice calculation, the CFS runtime must also be adapted. Here is the new formula, which takes the actual run time that process $i$ has accrued ($runtime$) and scales inversely by the weight of process $i$. In our running example, A's runtime will accumulate one-third of B's.

```
$runtime = runtime, + \frac{weight_0}{weight_i} \cdot runtime\quad (9.2)$
```

One smart aspect of the construction of the table of weights is that the table preserves CPU proportionality ratios when the difference in nice values is constant. For example, if A instead had a nice value of 5 (not -5), and process B had a nice value of 10 (not 0), CFS would schedule them exactly in the same manner as before. Run that yourself to see.

# Using Red-Black Trees

One major focus of CFS is efficiency, as stated above. For a scheduler, there are many facets of efficiency, but one of them is as simple as this: when the scheduler has to find the next job to run, it should do so as quickly as possible. Simple data structures like lists don't scale: modern systems are comprised of 1000s of processes, and searching through a long-list every few milliseconds is wasteful.

CFS addresses this by using balanced trees; in contrast to a simple binary tree (which can generate list-like performance under worst-case insertion patterns), balanced trees do a little extra work to maintain low depths, and ensure that operations are logarithmic (and not linear) in time. [B72].

CFS does not keep all process in this structure; rather, only running (runnable) processes are kept. If a process goes to sleep (say, waiting on an I/O to complete, or for a network packet to arrive), it is removed from the tree and kept elsewhere.

Let's look at an example to make this clear. Assume there are ten jobs, and they have the following values of $runtime$: 1, 5, 9, 10, 14, 18, 17, 21, 22, and 24. If we keep these in an ordered list, finding the next job to run would be simple: just insert the first element. However, placing job back into the list (in order), we would have to scan

> Yes, we are using bad bad grammar here on purpose, please don't find this in a bug fix. Why? Well, just a most of references to the Lord of the Rings, and our favorite anti-hero Gollum, not to get too excited.

OPERATING
SYSTEMS
[Version 1.01]

WWW.STEP.ORG