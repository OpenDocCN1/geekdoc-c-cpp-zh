# Distributed Algorithms

Some of the parallelism described in the previous sections are somewhat scarce. Very few home or business computers contain syntactic arrays (although I could see a case for building a chip to perform zero-time sorting). It may be decades before quantum computers appear in computer stores—if they ever do.

However, distributed computing is widely available. Large grid projects use tens or hundreds of thousands of computers to apply massive computing to complex problems. Smaller networked clusters let dozens of computers work together. Most desktop and laptop systems today contain multiple cores.

Some of these rely on fast communication between cores on a single chip, and others anticipate slow, unreliable network connections, but all these cases use distributed algorithms.

The next two sections discuss general issues that face distributed algorithms: debugging and identifying embarrassing parallel problems.

The sections after describe some of the most interesting classical distributed algorithms. Some of these seem more like IQ tests or riddles than practical algorithms, but they are useful for a couple of reasons. First, they highlight some the issues that affect distributed systems. They demonstrate ways to build about problems that encourage you to look for potential trouble spots in distributed algorithms.

Second, these algorithms are actually implemented in real-world scenarios. In many applications, it doesn't matter much if one of set of processes fails. If a grid computing process doesn't return a value, you can simply assign it to another computer and carry on. However, if a set of processors is controlling a patient's life-support systems, a large passenger plane, or a billion-dollar spacecraft, it may need the extra effort to ensure that the processes reach the correct decision, even if one of them produce incorrect results.

# Debugging Distributed Algorithms

Because events in different CPUs can occur in any order, debugging distributed algorithms can be very difficult. For example, consider the Hamiltonian path example described earlier. A race condition occurs only if the events in processes A and B happen in the exact right sequence. If the two processes don't update the shared best solution too frequently, the chance of they updating the solution at the same time is small. The two processes might run for a very long time before anything goes wrong.

Even if a problem does occur, you may not notice it. You'll detect the problem only if you notice that process B thinks the best solution is better than the currently saved solution. It's even possible that one of the processes will find a better solution and overwrite the incorrect one before you notice it.