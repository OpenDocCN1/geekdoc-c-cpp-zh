# Chapter 21

# Thread Pools

For performance reasons, threads are often pooled. Pooling helps reduce thread creation by reusing threads and makes it easier to place a bound on the number of active threads. A thread pool consists of generic workers that collectively execute the tasks submitted to the pool. Different types of thread pools exist, characterized by various properties: fixed or flexible number of workers, bounded or unbounded queue of tasks, scheduling and delaying facilities, and so on. Applications can use thread pools explicitly by submitting tasks directly to workers. Additionally, some languages define structures that can process their contents in parallel by submitting internal tasks to a thread pool. In functional and hybrid languages, this typically takes the form of parallel implementations of higher-order functions.

# 21.1 Fire-and-Forget Asynchronous Execution

Our discussion of concurrent programming began with a consideration of how threads can be created to introduce concurrency in an application. In all the examples so far, threads have been created with specific tasks that they run in parallel with other threads—such as printing a letter on the terminal or adding a string into a list. In practice, however, applications rarely start threads on a per-task basis. Instead, generic worker threads are pooled together, and tasks are submitted to them for execution.

This decoupling of threads and tasks has two main benefits. First, it makes it easier to control the number of threads created by an application. For instance, if a server creates a new thread with each incoming request, there is no upper bound on the number of threads that might be created, which can lead to poor performance and/or resource exhaustion. Second, thread creation and tear-down are not free. They tend to have a non-negligible runtime cost, which thread pools help amortize.

Instead of creating three threads to print the letters A, B, and C, as in Listing 17.1, you can create a thread pool first, and then submit letter-printing tasks to it:

```
Scala
println("START")

class LetterPrinter(letter: Char) extends Runnable:
  def run(): Unit = println(letter)

val exec = Executors.newFixedThreadPool(4)
```