
The allocation states for the system are decomposed in the accompanying Venn diagram in Figure 13.8. Observe that a safe state cannot be a deadlock state. One can also see that a state that is not safe is not necessarily a deadlock state but that it can lead to one. Let's look at a simple example.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_699_0.png)

Figure 13.8 Venn Diagram Illustrating Safe, Not Safe, and Deadlocked Situations

### EXAMPLE 13.1

We will look at a basic case first in which instances of a single resource are being allocated. Consider a system with an A/D that can accept and convert analog data from any one of 10 different inputs or channels. Using a multiplexer, we can connect signals from a number of different sources onto each input. Figure 13.9 illustrates such a design for a four-channel A/D converter.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_699_1.png)

Figure 13.9 An A/D Converter as a Shared Resource

In the four-channel design given, task T0 requires a maximum of three channels, task T1 requires two channels, task T2 three channels, task T3 two channels, and task T4 one channel.

Returning to the 10-channel system, three different tasks must use the A/D to make a number of different measurements. The tasks have the requirements and have been allocated the resources (channels) indicated in Figure 13.10.

The current state is safe. We have allocated eight of the channels and have two remaining. We can schedule the resources such that if we give the remaining two channels to T0, it can run to completion, freeing up five. Four of those five can then be given to task T2, allowing it to finish, and finally T1 can complete. We see that all tasks will eventually finish.

| Task | Maximum | Current |
|---|---|---|
| T0 | 5 | 3 |
| T1 | 4 | 1 |
| T2 | 8 | 4 |
| Total Allocated | | 8 |

Figure 13.10 Task Requirements and Allocations

### EXAMPLE 13.2

Let's now look at how a poor allocation can lead to an unsafe state. We start at the same initial state (see Figure 13.11).

| Task | Maximum | Current |
|---|---|---|
| T0 | 5 | 3 |
| T1 | 4 | 1 |
| T2 | 8 | 4 |
| Total Allocated | | 8 |

Figure 13.11 Task Requirements and a Poor Allocation

Rather than permitting T0 to run, a request from T1 for two additional channels is honored. Such an allocation allows T1 to continue for a short while. However, when it issues a request for the last resource that it needs, there are none available. Furthermore, the other two tasks are blocked as well, and a deadlock now exists.

Thus, the allocation given in Figure 13.11 can lead to an unsafe state.

With the luxury of hindsight, these two examples show that a safe state is one in which there is at least one resource allocation sequence that will allow all tasks to finish eventually. One can also see that the existence of an unsafe state does not inherently lead to a deadlock. It does show that, with an improper allocation, such a condition can occur.

## 13.9 DEADLOCK DETECTION

If the system utilizes neither a prevention nor an avoidance algorithm, a deadlock may occur. In such an environment, the system must provide an algorithm to determine whether such a state has occurred as well as one to recover from the deadlock.

### 13.9.1 Detection in a Single-Instance Environment

When designing a system in which there is a single instance of each resource, then, as was done earlier, one can begin with the resource allocation graph. From the resource allocation graph, a **wait-for graph** is developed by removing the nodes of type resource and then collapsing the edges as appropriate. The result of such a process is a graph with only processes; a deadlock then exists if and only if the reduced graph contains a cycle.

Starting with the resource allocation graph, the left-hand graph in Figure 13.12, the set of resources {R1 ... R6} is removed. Removal of those nodes results in the reduced graph in the right-hand figure.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_701_0.png)

Figure 13.12 A Resource Allocation Graph and the Associated Wait-for Graph

It is immediately evident that the graph on the right has several cycles and, thus, has a number of processes in the deadlock state.

### 13.9.2 Deadlock Recovery

When it has been determined that a deadlock exists, the objective changes from detection to recovery. Several courses of action are open. Ignoring the deadlock is not one of the reasonable alternatives. One can always inform the users that such a situation exists and let them handle it. Such an approach is often difficult in an embedded system. Another possibility is to let the system recover automatically. Selecting automatic recovery leads to two general schemes: a termination signal can be sent to all deadlocked processes (one at a time), or the processes can be preempted one at a time and their resources temporarily taken.

### 13.9.2.1 Task Termination

The drastic approach of terminating all deadlocked processes will clearly have the desired effect, but at significant cost, since the tasks may have been running for some time. Following such an action, it is most likely that all results may be lost. On the other hand, terminating processes, one at a time, until a deadlock cycle is eliminated involves considerable temporal overhead. As each process is aborted, the deadlock detection algorithm must be rerun.

Extreme care must be taken when terminating a task because doing so may leave a resource or the system in an unknown, unusable, or dangerous state. One must also determine which process to terminate. The problem is similar to that encountered when trying to schedule usage of the CPU. The objective is to terminate processes so as to do the least damage, incur minimal cost, and ensure an efficient recovery. Some things to consider include:

- Task priority.
- The time since starting the task and the remaining runtime.
- The resource mix and quantity.
- The resource demand to complete.
- The number of tasks/threads to be terminated.

### 13.9.2.2 Resource Preemption

The process preemption alternative to termination entails successive preemption of the task and its resources and their subsequent allocation to other processes until the deadlock cycle is broken. If preemption is used, three issues must be considered.

- 1. Selection of a task to preempt.
  One must determine the order of preemption to minimize the cost. When making such a decision, the same factors are considered as when process termination is assessed.
- 2. Rollback.
  If a resource is preempted, what should be done with the preempted task? Certainly, it cannot continue from its current state. One alternative that can be used is the same as that used when developing software or writing long documents. A backup is saved periodically. Such a backup gives a snapshot of the state of the system called a checkpoint. When a process and its resources must be preempted, it can be restarted – rolled back – sometime in the future to the last checkpoint. All resources and the state of the process are restored to values at the last checkpoint. However, one may not be able to determine a completely safe internal state of the system or for external devices being controlled. It is rather tricky to roll back the temperature of a chemical process or the yeast in a fermenting batch of beer in a brewery and hold it for a little while. Such factors must be taken into consideration when deciding which processes to preempt. Generally, the simplest solution is a complete rollback, subject, of course, to the earlier considerations. That is, abort the task and restart it.

One can try to roll back as far as necessary to break the deadlock. Such a strategy entails maintaining information on all the running tasks and threads.

- 3. Starvation.
  How does one ensure starvation will not occur? One strives to ensure that the resources are not always preempted from the same process.

## 13.10 SUMMARY

Deadlock occurs when two or more processes are waiting for an event that can only be caused by one of the waiting processes. There are three major methods for addressing the problem.

- 1. Use a protocol to ensure that the system will never enter a deadlock state.
- 2. Allow the system to enter a deadlock state and then recover.
- 3. Ignore the problem.

Deadlock occurs if, and only if, four conditions (mutual exclusion, hold and wait, no preemption, and circular wait) occur simultaneously. We prevent deadlock by ensuring that one of the conditions will not occur.

If a system does not employ a protocol to ensure that deadlock does not occur, then a detection and recovery scheme of some form or another must be employed. If a deadlock is detected, we can recover by global or selective termination of tasks (threads) or resources.

## 13.11 REVIEW QUESTIONS

### A Model of Tasks and Resources

- 13.1 What is a deadlock in an embedded application?
- 13.2 What is the typical protocol that a task will use for handling resources?
- 13.3 What is the difference between deadlock and starvation?

### A Deadlock Model

- 13.4 What are the necessary conditions for a deadlock to occur?
- 13.5 Give a real-world example in which a deadlock can occur.
- 13.5 What is a resource allocation graph?
- 13.6 Within a resource allocation graph, what is a request edge? an allocation edge?

### Deadlock Prevention

- 13.8 Describe the conditions under which the necessary condition hold and wait cannot occur.
- 13.9 Describe the conditions under which the necessary condition no preemption cannot occur.
- 13.10 Describe the conditions under which the necessary condition circular wait cannot occur.

### Deadlock Avoidance

- 13.11 What strategy underlies most deadlock avoidance algorithms?
- 13.12 One strategy for avoiding deadlock utilizes a modified allocation graph. Describe that strategy.
- 13.13 In the context of the banker's algorithm, what is a resource allocation state?
- 13.14 Under what conditions is a resource allocation state defined as safe?
- 13.15 What is a safe sequence?
- 13.16 What is an unsafe state?
- 13.17 Can a safe state be a deadlock state?
- 13.18 Is an unsafe state guaranteed to be a deadlock state?

### Deadlock Detection

- 13.19 What is a wait-for graph?
- 13.20 How is a wait-for graph developed? What does a cycle in a wait-for graph imply?
