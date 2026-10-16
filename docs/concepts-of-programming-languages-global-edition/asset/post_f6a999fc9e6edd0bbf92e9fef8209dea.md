
The following are concise pseudocode descriptions of wait and release:

```
wait(aSemaphore)
if aSemaphore's counter > 0 then
  decrement aSemaphore's counter
else
  put the caller in aSemaphore's queue
  attempt to transfer control to some ready task
  (if the task-ready queue is empty, deadlock occurs)
end if
```

```
release(aSemaphore)
if aSemaphore's queue is empty (no task is waiting) then
  increment aSemaphore's counter
else
  put the calling task in the task-ready queue
  transfer control to a task from aSemaphore's queue
end
```

We can now present an example program that implements cooperation synchronization for a shared buffer. In this case, the shared buffer stores integer values and is a logically circular structure. It is designed for use by possibly multiple producer and consumer tasks.

The following pseudocode shows the definition of the producer and consumer tasks. Two semaphores are used to ensure against buffer underflow or overflow, thus providing cooperation synchronization. Assume that the buffer has length BUFLEN, and the routines that actually manipulate it already exist as FETCH and DEPOSIT. Accesses to the counter of a semaphore are specified by dot notation. For example, if fullspots is a semaphore, its counter is referenced by fullspots.count.

```
semaphore fullspots, emptyspots;
fullspots.count = 0;
emptyspots.count = BUFLEN;
task producer;
  loop
    -- produce VALUE --
    wait(emptyspots);      { wait for a space }
    DEPOSIT(VALUE);
    release(fullspots);    { increase filled spaces }
  end loop;
end producer;
```

```
task consumer;
  loop
    wait(fullspots);       { make sure it is not empty }
```

```
FETCH (VALUE);
release(emptyspots); { increase empty spaces }
-- consume VALUE --
end loop
end consumer;
```

The semaphore fullspots causes the consumer task to be queued to wait for a buffer entry if it is currently empty. The semaphore emptyspots causes the producer task to be queued to wait for an empty space in the buffer if it is currently full.

## 13.3.3 Competition Synchronization

Our buffer example does not provide competition synchronization. Access to the structure can be controlled with an additional semaphore. This semaphore need not count anything but can simply indicate with its counter whether the buffer is currently being used. The wait statement allows the access only if the semaphore's counter has the value 1, which indicates that the shared buffer is not currently being accessed. If the semaphore's counter has a value of 0, there is a current access taking place, and the task is placed in the queue of the semaphore.

Notice that the semaphore's counter must be initialized to 1. The queues of semaphores must always be initialized to empty before use of the queue can begin.

A semaphore that requires only a binary-valued counter, like the one used to provide competition synchronization in the following example, is called a binary semaphore.

The example pseudocode that follows illustrates the use of semaphores to provide both competition and cooperation synchronization for a concurrently accessed shared buffer. The access semaphore is used to ensure mutually exclusive access to the buffer. Remember that there may be more than one producer and more than one consumer.

```
semaphore access, fullspots, emptyspots;
access.count = 1;
fullspots.count = 0;
emptyspots.count = BUFLEN;
task producer;
loop
-- produce VALUE --
wait(emptyspots); { wait for a space }
wait(access); { wait for access }
DEPOSIT(VALUE);
release(access); { relinquish access }
release(fullspots); { increase filled spaces }
end loop
end producer;
```

```
task consumer;
  loop
    wait(fullspots);      { make sure it is not empty }
    wait(access);         { wait for access }
    FETCH(VALUE);
    release(access);      { relinquish access }
    release(emptyspots); { increase empty spaces }
    -- consume VALUE --
  end loop
end consumer;
```

A brief look at this example may lead one to believe that there is a problem. Specifically, suppose that while a task is waiting at the wait(access) call in consumer, another task takes the last value from the shared buffer. Fortunately, this cannot happen, because the wait(fullspots) reserves a value in the buffer for the task that calls it by decrementing the fullspots counter.

There is one crucial aspect of semaphores that thus far has not been discussed. Recall the earlier description of the problem of competition synchronization: Operations on shared data must not overlap. If a second operation begins while an earlier operation is still in progress, the shared data can become corrupted. A semaphore is itself a shared data object, so the operations on semaphores are also susceptible to the same problem. It is therefore essential that semaphore operations be uninterruptible. Many computers have uninterruptible instructions that were designed specifically for semaphore operations. If such instructions are not available, then using semaphores to provide competition synchronization is a serious problem with no simple solution.

## 13.3.4 Evaluation

Using semaphores to provide cooperation synchronization creates an unsafe programming environment. There is no way to check statically for the correctness of their use, which depends on the semantics of the program in which they appear. In the buffer example, leaving out the wait(emptyspots) statement of the producer task would result in buffer overflow. Leaving out the wait(fullspots) statement of the consumer task would result in buffer underflow. Leaving out either of the releases would result in deadlock. These are cooperation synchronization failures.

The reliability problems that semaphores cause in providing cooperation synchronization also arise when using them for competition synchronization. Leaving out the wait(access) statement in either task can cause insecure access to the buffer. Leaving out the release(access) statement in either task results in deadlock. These are competition synchronization failures. Noting the danger in using semaphores, Per Brinch Hansen (1973) wrote, “The semaphore is an elegant synchronization tool for an ideal programmer who never makes mistakes.” Unfortunately, ideal programmers are rare.

## 13.4 Monitors

One solution to some of the problems of semaphores in a concurrent environment is to encapsulate shared data structures with their operations and hide their representations—that is, to make shared data structures abstract data types with some special restrictions. This solution can provide competition synchronization without semaphores by transferring responsibility for synchronization to the run-time system.

### 13.4.1 Introduction

When the concepts of data abstraction were being formulated, the people involved in that effort applied the same concepts to shared data in concurrent programming environments to produce monitors. According to Per Brinch Hansen (Brinch Hansen, 1977, p. xvi), Edsger Dijkstra suggested in 1971 that all synchronization operations on shared data be gathered into a single program unit. Brinch Hansen (1973) formalized this concept in the environment of operating systems. The following year, Hoare (1974) named these structures monitors.

The first programming language to incorporate monitors was Concurrent Pascal (Brinch Hansen, 1975). Modula (Wirth, 1977), CSP/k (Holt et al., 1978), and Mesa (Mitchell et al., 1979) also provide monitors. Among contemporary languages, monitors are supported by Ada, Java, and C#, all of which are discussed later in this chapter.

### 13.4.2 Competition Synchronization

One of the most important features of monitors is that shared data is resident in the monitor rather than in any of the client units. The programmer does not synchronize mutually exclusive access to shared data through the use of semaphores or other mechanisms. Because the access mechanisms are part of the monitor, implementation of a monitor can be made to guarantee synchronized access by allowing only one access at a time. Calls to monitor procedures are implicitly blocked and stored in a queue if the monitor is busy at the time of the call.

### 13.4.3 Cooperation Synchronization

Although mutually exclusive access to shared data is intrinsic with a monitor, cooperation between processes is still the task of the programmer. In particular, the programmer must guarantee that a shared buffer does not experience underflow or overflow. Different languages provide different ways of programming cooperation synchronization, all of which are related to semaphores.

A program containing four tasks and a monitor that provides synchronized access to a concurrently shared buffer is shown in Figure 13.3. In this figure,
