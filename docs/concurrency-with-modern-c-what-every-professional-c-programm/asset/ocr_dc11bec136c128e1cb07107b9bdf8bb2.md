# ### 7.4.4 The Scheduler

The scheduler manages which thread is running. This means that it is no longer the responsibility of the programmer to decide who executes the task. Threads are just an implementation detail.

There are two strategies for executing the newly created task. The parent represents the creator thread and the child the new task.

+   Child stealing
+       The scheduler steals the task and executes it.
+   Parent stealing
+       The task block to itself executes the task. Now the scheduler steals the parent.

Proposal N4441^{15} supports both strategies.