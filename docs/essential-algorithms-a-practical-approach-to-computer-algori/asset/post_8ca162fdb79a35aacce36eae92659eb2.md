
# Chapter 18 Distributed Algorithms 439

try to minimize communication between the computers. Typically a distributed algorithm sends data to the computers, the computers spend some time working on the problem, and then they send back a solution.

Two kinds of distributed environments are cluster and grid computing. A cluster is a collection of closely related computers. Often they are connected by an intranet or a special-purpose network that has limited access to outside networks. For many practical purposes, you can think of a cluster as a giant computer that has unusual internal communications.

In grid computing, the collection of computers is much less tightly integrated. They may communicate over a public network and may include different kinds of computers running different operating systems.

Communications among the computers in grid computing can be quite slow and may be unreliable. Because the computers are only loosely associated, any given computer may not finish its assigned calculations before its owner shuts down, so the system needs to be reassign subproblems to others if necessary.

Despite the drawbacks of relatively slow communications and the unreliability of individual computers, grid computing allows a project to create a "virtual supercomputer" that can potentially enhance enormous amounts of processing power to a problem. The following list summarizes some grid projects:

- MilkyWay@home
http://milway.cs.rpi.edu/milkyway

This project is building a very accurate model of the Milky galaxy for use in astrophysics and computer science research. This research has 38,000 or so computers provide about 1.6 petaflops.

- Berkeley Open Infrastructure for Network Computing (BOINC)
http://boinc.berkeley.edu

This open source project is used by many separate projects to study problems in astrophysics, mathematics, medicine, chemistry, biology, and other fields. Its roughly 600,000 computers provide about 9.2 petaflops.

- Folding@home
http://folding.stanford.edu

This project models protein folding in an attempt to understand diseases such as Alzheimer’s, mad cow (BSE), Huntington’s, Parkinson’s, and many cancers. This projects almost 200,000 computers provide about 12 petaflops.

## FLOPS

The speed of computers that are used to perform intensive mathematical calculations is measured in floating-point operations per second (flops). One teraflop (tflop) is 10¹² flops, or 1 trillion flops. One petaflop (pflop) is 10¹⁵ flops. For comparison, a typical desktop system might be able to run in the 0.25 to 10 gigaflops range.

## JOINING A GRID

If you're interested in these projects, visit their web pages to download software that will let your computer contribute CPU cycles when it's idle.

Because the processes on distributed computers can execute different tasks, this approach demonstrates task parallelism. Contrast this with data parallelism, in which the focus is distributing data across multiple processors.

## Multi-CPU Processing

Most modern computers include multiple processors. Sometimes these are on separate chips, but often they are multiple cores on a single chip.
CPUs on the same computer can communicate more quickly than computers in a distributed network, so some of the communications problems that can trouble distributed networks don't apply. For example, a distributed network must pass the least data between computers so by communication speeds. In contrast, CPUs in the same computer can communicate very quickly, so they can exchange data without paying a big performance penalty.

Multiple CPUs on the same computer can also access the same disk drive and memory.

The ability to exchange more data and to access the same memory and disks can be helpful, but it can also lead to problems such as race conditions and deadlock. These can happen with any distributed system, but they're most common in multi-CPU systems because it's so easy for the CPUs to contend for the same resources.

## Race Conditions

In a race condition, two processes try to write to a resource at almost the same time. The process that writes to the resource second wins.

To see how this can happen, suppose two processes use heuristics to solutions to the Hamiltonian problem (discussed in Chapter 17) and then use the following pseudocode to update shared variables that hold the best route so far and that route's total length:

```
// Perform heuristics.
...
// Save the best solution.
If (test_length < BestLength) Then
    // Save the new solution.
```

```
// Save the new total length.
BestLength = test_length
End If
```

The pseudocode uses heuristics to find a good solution. It then compares the best total route it found the value stored in the shared variable BestLength. If the new solution is better than the previous best, the pseudocode saves the new solution and the new route's length.
Unfortunately, you cannot tell when the multiple processes will actually access the shared memory. Suppose two processes happen to execute their code in the order shown in the following pseudocode timeline:

```
// Perform heuristics
Perform heuristics
```

```
// Save the best solution.
If (test_length < BestLength) Then
```

```
// Save the best solution.
If (test_length < BestLength) Then
```

```
// Save the new solution.
```

```
// Save the new solution.
Save the new total length.
BestLength = test_length
End If
```

```
// Save the new total length.
BestLength = test_length
End If
```

The timeline shows the actions performed by process A on the left and performed by B on the right.
\Process A then executes the If test to see whether it found an improved solution. Suppose for this example that the initial best solution had a route length of 100, and process A found a route with a total length of 70. Process A enters the If block.
Next, process B executes its If test. Suppose process B finds a route with total length of 90, it also enters its If block.
Process A saves its solution.
Next, process B saves its solution. It also updates the shared variable BestLength to the new route's length: 90.

Now process A updates BestLength to the length of the route found: 70. At this point the shared solution holds B's solution, which is the worse of the two solutions the processes found. The variable BestLength also holds the value 70, which was actually saved.

You can prevent race conditions by using a mutex. A mutex (the name from "mutual exclusion") is a method of ensuring that only one process can perform a certain operation at a time.

## IMPLEMENTING MUTEXES

Some computers may provide hardware making mutexes more efficient. On other computers, mutexes must be implemented in software.

The following pseudocode shows how you add a mutex to the previous algorithm to prevent the race conditions:

```
// Perform heuristics.
...

// Acquire the mutex.
...
// Save the best solution.
If (test_length < BestLength) Then
    // Save the new solution.

    // Save the new total length.
    BestLength = test_length
End If

// Release mutex.
...
```

In this version of the code, the process performs its heuristics as before. It does without any shared memory. Exactly how that depends on the programming language you are using. For example, in the .NET languages C# and Visual Basic, a process can create a Mutex object and use its WaitOne method to request ownership of the mutex.

If another process tries to acquire the mutex at this point, it blocks and waits until the mutex is released. After the process acquires the mutex, it manipulates the shared memory. Because no other process can acquire the mutex at this point, it cannot change the shared memory while the first process is using it.

When it has finished examining and updating the shared solution, the process releases the mutex so that any other process that is waiting for it can continue.
The following code shows what happens if the earlier sequence of events occurs while processes A and B are using a mutex:

```
// Perform heuristics.
..
```

```
// Perform heuristics.
...
```

```
// Acquire the mutex.
...
// Save the best solution.
If (test_length < BestLength) Then
```

```
// Process B attempts to acquire
// the mutex, but process A already
// owns it, so process B is blocked.
```

```
// Save the new solution.
...
// Save the new total length.
BestLength = test_length
End If
```

```
// Release the mutex.
...
```

```
// Process B acquires the mutex, is
// unblocked and continues running.
```

```
// Save the best solution.
If (test_length < BestLength) Then
// Save the new solution.

```
// Save the new total length.
BestLength = test_length
End If
```

```
// Release the mutex.
...
```

Now the two processes do not interfere with each other’s use of the shared memory, so there is no race condition.
