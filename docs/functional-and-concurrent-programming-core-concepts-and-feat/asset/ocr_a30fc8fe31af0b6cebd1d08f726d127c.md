# Chapter 17

# Threads and Nondeterminism

Sequential programs have a single thread of execution. Programs can be made concurrent by creating additional threads so that multiple threads execute a program in parallel. How threads access hardware computing resources is typically orchestrated by a scheduler—often in the operating system—which is not under a programmer’s control. As a result, and in the absence of additional synchronization, the exact order in which multiple threads jointly execute their instructions is unpredictable. Consequently, multithreaded programs tend to exhibit nondeterministic behavior. This nondeterminism vastly complicates testing and debugging.

# 17.1 Threads of Execution

A thread of execution—or thread, for short—represents the execution of a series of instructions. Programs often start with a single thread¹ and terminate when this thread is finished. The program

```
Scala
import tinyscalautils.text.{ println, threadTimeDemoMode }

println("START")
println("END")
```

produces an output of the following form:

```
main at XX:XX:14.216: START
main at XX:XX:14.217: END
```

This program relies on a println function that is defined to add thread and timing information to the message being displayed.² Here, a thread called “main,” created and started by the JVM, executes both statements in sequence, within a few milliseconds, at which point the program ends and the JVM terminates.

To create additional threads (besides main), Java defines a Thread class, and JVM languages rely on Java’s mechanisms for thread creation. You instantiate the Thread

¹More precisely, user code is executed within a single thread of execution. Typically, a JVM uses additional threads for garbage collection, just-in-time compilation, and other operations.

²In the following chapters, many code examples use this modified println function—or its printf variant—without importing it explicitly.