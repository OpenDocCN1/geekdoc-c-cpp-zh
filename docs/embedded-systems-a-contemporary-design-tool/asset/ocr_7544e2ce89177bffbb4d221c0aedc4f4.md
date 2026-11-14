The major difference between the monitor and a class in C++ or Java is that the monitor is shared by multiple concurrently executing processes or threads. Consequently, the threads or processes using a monitor may require mutual exclusion to the monitor variables as well as synchronization to ensure that the monitor state is conducive to continued execution.

Mutual exclusion is usually implicit; synchronization is implemented explicitly. Different processes require different forms of synchronization. The implementation of the necessary synchronization is accomplished through condition variables. An external task or thread calls a monitor procedure. The procedure is active if a thread or task is executing a statement in the procedure. At most, one instance of a monitor procedure is active at any one time. The simultaneous invocation of two different procedures or two invocations of the same procedure is not permitted.

By definition, the procedures execute with mutual exclusion that is ensured by the language library and operating system. Mutual exclusion is generally implemented by using locks or semaphores and by inhibiting certain interrupts.

# 12.10.1 Condition Variables

Condition variables are used as part of the synchronization process and are intended to delay a task or thread that cannot safely continue until the monitor's state satisfies some Boolean condition. Note that condition variables are similar to the guard conditions in Unified Modeling Language (UML) state charts. They are then used to awaken the delayed process once the condition becomes true. A condition variable is an instance of a variable of type cond.

```
cond myCondVar;
```

The declaration can only occur inside the monitor. The value of the condition variable is a queue of delayed processes. Initially, the queue is empty. The value on the queue can only be accessed indirectly, for example, to test its state.

```
empty(myCondVar);
```

A thread can block on a condition variable:

```
wait(myCondVar);
```

Execution of the wait causes the task to move to the rear of the queue and to relinquish exclusive access to the monitor. A blocked process is awakened using

```
signal(myCondVar);
```

Execution of a signal causes the task at the head of the queue to awaken.

Observe that the execution of signal seems to cause a dilemma. Upon execution, two tasks have the potential to execute: the awakened task and the signaling task. Such a situation seems to contradict the requirement that only a single task or thread can be active in the monitor at any one time.

There are two possible paths for resolution:

+   - Signal and Continue. The signaling task continues, and the awakened task resumes at some later time. Such a scheme is considered nonpreemptive; the process executing the signal retains exclusive control of the monitor.