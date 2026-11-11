A rendezvous can occur in two basic ways in this simple example. First, the receiver task, Task_Example, can be waiting for another task to send a message to the Entry_1 entry. When the message is sent, the rendezvous occurs. This is the situation described earlier. Second, the receiver can be busy with one rendezvous, or with some other processing not associated with a rendezvous, when another task attempts to send a message to the same entry. In that case, the sender is suspended until the receiver is free to accept that message in a rendezvous. If several messages arrive while the receiver is busy, the senders are queued to wait their turn for a rendezvous.

The two rendezvous just described are illustrated with the timeline diagrams in Figure 13.4.

![](bbox=[0.03, 0.28, 0.98, 0.79])

Tasks need not have entry points. Such tasks are called actor tasks because they do not wait for a rendezvous in order to do their work. Actor tasks can rendezvous with other tasks by sending them messages. In contrast to actor tasks, a task can have accept clauses but not have any code outside those accept clauses, so it can only react to other tasks. Such a task is called a server task.

An Ada task that sends a message to another task must know the entry name in that task. However, the opposite is not true: A task entry need not