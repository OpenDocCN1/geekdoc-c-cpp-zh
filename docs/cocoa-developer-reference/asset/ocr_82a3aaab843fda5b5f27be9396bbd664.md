Figure 18.18 shows Shark profiling the performance of the Firefox Web browser. Shark doesn’t include filters that distinguish between custom code and processes that are internal to OS X, so you must pick through this list by hand.

Shark works best for simple projects with relatively small numbers of competing processes. As the process and event count increases, the profiling becomes diluted and less useful.

# Figure 18.18

Shark versus Firefox. Shark is only sporadically useful. In this example, Firefox was suffering from processor spiking, but it’s not easy to find the culprit from this trace.

![](bbox=[0.162, 0.302, 0.819, 0.663])

# Managing Code with Snapshots and Source Control

It’s often useful to create multiple versions of a project while debugging. It’s easier to remove temporary debugging code by reverting to an older version than by manually removing the additions.