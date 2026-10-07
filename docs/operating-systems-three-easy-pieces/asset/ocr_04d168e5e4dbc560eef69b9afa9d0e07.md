# SCHEDULING:

THE MULTI-LEVEL FEEDBACK QUEUE

![](bbox=[0.318, 0.143, 0.681, 0.329])

Figure 8.4: A Mixed I/O-intensive and CPU-intensive Workload
inserted into the highest queue; as its run-time is short (only 20 ms), B
completes before reaching the bottom queue, in two time slices; then A
resumes running (at low priority).

From this example, you can hopefully understand one of the major
goals of the algorithm: because it doesn't know whether a job will be a
short job or a long-running job, it *first assumes* it might be a short job, thus
giving the job high priority. If it is actually a short job, it will run quickly
and complete; if it is not a short job, it will slowly move down the queues,
and thus proves itself to be a long-running more batch-like process.
in this manner, MLQ approximates SJ.

# Example 3: What About I/O?

Let's now look at an example with some I/O. As Rule 4b states, if a
rocess gives up the processor before using its time slice, we keep it at
t same priority. The intent of this rule is simple: if an interactive
job, for example, is doing a lot of I/O (say by waiting for user input from
keyboard or mouse), it will relinquish the CPU before its time slice is
complete; in such case, we don't penalize the job and thus simply
keep it at the same level.

Figure 8.5 (in gray) shows an example of how this works, with an interactive job
B (in gray) that needs the CPU for only 1 ms before performing an
I/O competing with a long-running batch job A (in black). The MLQ approach keeps B at the highest priority because B
releasing the CPU; if B is an interactive job, MLQ further achieves
it goal of running interactive jobs quickly.

# Problems With Our Current MLQ

We have a basic MLQ It seems to be a good job, sharing the
CPU fairly between long-running jobs, and letting short or I/O-intensive
interactive jobs run quickly. Unfortunately, the approach we have devel-
oped far contains several flaws. Can you think of any?
(This is where you pause and think as deviously as you can)

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIES