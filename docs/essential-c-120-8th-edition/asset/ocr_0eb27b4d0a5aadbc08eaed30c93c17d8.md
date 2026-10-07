Multithreading Basics 941

# Uncertainty Caused by Race Conditions

As we discussed earlier, concurrency is often simulated by time slicing. In the absence of special thread synchronization (which we discuss in detail in Chapter 22), the operating system can switch contexts between any two threads at any time of choosing. As a consequence, when two threads are accessing the same object, which thread wins the race and gets to run is unpredictable. If there are two threads running in the code fragment given previously, for example, it is possible that one thread might win the race and get all the way to the end before the second thread a chance to run. It is also possible that the context switch might happen after the first thread does the balance check, and the second thread might then win the race to get all the way to the end first.

The behavior of code that contains race conditions depends on the timing of context switches. This dependency introduces uncertainty concerning program execution. The order in which one instruction will execute relative to an instruction in a different thread is unknown. The worst of it is that code containing race conditions often behaves 99.9 percent of the time, and then one in a thousand different thread wins the race due to an accident of timing. This unpredictability is what makes multithreaded programming so difficult.

Because such race conditions are difficult to replicate in the laboratory, much of the quality assurance of multithreaded code depends on long-running stress tests, specially designed code analysis tools, and a significant investment in code analysis and review by experts. Perhaps more important than any of these is the discipline of keeping things as simple as possible. Often, in the manner of hypothetical performance, a developer will try to avoid the simple approach of using a lock and go for lower-level primitives such as interlocked operations and volatiles, which makes it more likely that their code is wrong. "Keep it simple" is possibly one of the most important guidelines of good multithreaded programming.

Chapter 22 is about techniques for dealing with race conditions.

# Memory Models Are Complex

The existence of race conditions, where two points of control can "race" through a piece of code at unpredictable and inconsistent speeds, is bad enough, but it gets