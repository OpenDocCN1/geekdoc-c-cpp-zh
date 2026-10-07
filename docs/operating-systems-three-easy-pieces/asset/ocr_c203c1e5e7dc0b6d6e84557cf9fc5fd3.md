# SCHEDULING: PROPORTIONAL SHARE

> TIP: USE EFFICIENT DATA STRUCTURES WHEN APPROPRIATE
in many cases, a list will do. In many cases, it will not. Knowing which data structure to use is a hallmark of good engineering. In the case discussed here, simple lists found in earlier schedulers simply do not work well on modern systems, particularly in the heavily loaded servers of datacenters. Such systems contain thousands of active processes; searching through a long list to find the next job to run every few milliseconds would waste precious CPU cycles. A better structure was needed, and CFS provided one by an excellent implementation of a red-black tree. More generally, picking a data structure for a system you are building, carefully consider its access patterns and its frequency of use; by understanding these, you will be able to implement the right structure for the task at hand.

# 9.8 Summary

We have introduced the concept of proportional-share scheduling and briefly discussed three approaches: lottery scheduling, stride scheduling, and the Completely Fair Scheduler (CFS) of Linux. Lottery uses randomness in a clever way to achieve proportional share; stride, the only “real” scheduler does so deterministically, with bit like weighted round-robin slices, but built to scale and perform well under load; to our knowledge, it is the most widely used fair-share scheduler in existence today.

No scheduler is perfect, and fair-share schedulers have their fair share of problems. One issue is that these approaches do not particularly mesh with I/O [AC97]; as mentioned above, jobs that perform I/O occasionally may not get their share of CPU. Another issue is that they leave the hard problem of ticket or priority assignment, i.e., to what value set your tickets to your text editor? Other general-purpose schedulers (such as the MLFQ we discussed previously, and other Linux schedulers) handle these automatically and may be more easily deployed.

The good news is that there are many domains in which these problems are not the dominant concern, and proportional-share schedulers are used to great effect. For example, in a virtualized data center (or cloud), where you might like to assign one-quarter of your CPU cycles to the Windows VM and the rest to your base Linux installation, proportional sharing can be simple and effective. The idea could also be extended to other resources; see Waldspurger [W02] for further details on how to proportionally share memory in VMware’s ESX Server.

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG