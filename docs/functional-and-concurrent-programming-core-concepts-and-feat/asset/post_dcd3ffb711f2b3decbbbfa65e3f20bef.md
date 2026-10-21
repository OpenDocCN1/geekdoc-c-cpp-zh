
### 27.8 Summary

- When programming with synchronizers, such as locks, latches, and futures, threads can be temporarily blocked while other threads perform an operation, which often results in non-negligible performance loss. Chapter 26 presented a programming style that uses futures in a functional way, without blocking threads. Some other techniques minimize thread blocking, as discussed in this chapter.
- Compare-and-set (CAS) is a hardware instruction that implements an elementary atomic check-then-act operation. It is also available on language-level types like `AtomicInteger` and `AtomicReference` as a `compareAndSet` method. It can be used to implement other thread-safe operations, such as `incrementAndGet` and `getAndSet` in class `AtomicInteger`.
- In particular, class `AtomicReference` and atomic updaters make it possible to manipulate pointers atomically without going through locks. This is the basis for various lock-free algorithms that implement thread-safe data structures without locking, albeit at the cost of increased code complexity.
- Lock-free algorithms tend to follow a similar pattern. Computation proceeds without locking, and thus with no guarantee that other threads will not interfere. Work is performed speculatively and then committed using CAS. A failed CAS is an indication that interference from other threads did take place, in which case the operation can be reattempted.
- Functional-concurrent programming avoids blocking threads by using futures through callbacks and higher-order functions. An alternative approach is to make it possible for code to explicitly wait for completion of a future, but without blocking a thread. Many different implementations of this principle are possible. Java’s `ForkJoinTask`, for instance, implements a kind of future with a `join` method that suspends code execution until the future terminates, but does not block the running thread, leaving it free to execute other tasks in the pool. This results in a programming style that often feels more natural—resembling a blocking variant—than one that relies on callbacks and scheduled transformations.
- This idea of waiting without blocking is sometimes extended beyond futures and made available in other flavors, such as *async/await* constructs and coroutines. In addition to waiting for a value produced by a task, these constructs offer non-blocking ways to wait for a message from a channel, or to acquire an exclusive lock, for instance.
- Actors are a model of concurrent and distributed programming centered on messages. Actors send and receive messages, which are handled sequentially within an actor, making it possible to use non-thread-safe code during message processing. Passive actors, with no pending messages, use no computing resources. They do not block threads, which remain available to run active actors.
- Frameworks also exist to process streams of data in parallel while avoiding thread blocking when data is not available. Reactive streams complement futures—which eventually either produce a single value or fail—by being able to produce zero or more values before they terminate. A generic reactive streams specification (www.reactive-streams.org) has been implemented in a variety of programming languages.
- When code does not block threads, performance often improves, and many synchronization mistakes common to programming with locks are avoided. Non-blocking approaches, however, are not fool-proof. Concurrent entities still need to correctly coordinate to achieve overall computational objectives. In particular, synchronization mistakes can still result in deadlocks—of futures, coroutines, or actors—even if the underlying threads are not blocked.

This page intentionally left blank

## Chapter 28: Case Study: Parallel Strategies

Our final case study expands on the previous one by focusing on the parallel execution of functions—as opposed to the actions examined in Chapter 24. It considers a scenario in which several functions are applied to the same input, each with a different likelihood of succeeding. The implementation leverages the concurrency constructs explored in earlier chapters—promises, futures, higher-order functions—and uses their features to address failure, timeout, cancellation, and caching issues.

### 28.1 Problem Definition

> **NOTE**
>
> This case study was inspired by a problem I faced, a long time ago, while working on static analysis of programs. I was implementing a tool that worked by generating proof obligations—that is, logical formulas that need to be valid to show that a program satisfies a desirable property. The formulas were typically large, numerous, and costly to verify. My tool used automatic theorem provers to check the validity of the formulas, but different theorem provers—and different configurations of the same theorem prover—would often perform very differently on the same formula. With no way to predict which prover would work best, several theorem provers were started in parallel on each formula and stopped as soon as one prover found the formula to be valid or invalid. Some of the assumptions made in this chapter reflect the particulars of this theorem-proving scenario.

This last case study investigates a scenario in which a series of problems need to be solved using a variety of heuristics. For a given problem, you don’t know which heuristic will work, so you would like to try several heuristics in parallel until one succeeds. In this chapter, heuristics are represented in terms of a Strategy interface:

```scala
trait Strategy[A, B]:
  trait Task:
    def run(): Option[B]
    def cancel(): Unit

  def apply(input: A): Task
```

Strategies are parameterized by an input type A and an output type B. (In the program verification problem, type A would represent logical formulas, and type B would be Boolean.) When applied to a given input, a strategy produces a task, which can be run in an attempt to calculate the corresponding output. A task may succeed or fail, and thus returns an option. A task can also be canceled—for instance, because it has exceeded its time quota, or because another strategy has already solved the problem. The code developed in this chapter hinges on several assumptions:

- A strategy can only succeed with a value, fail by returning an empty option, or keep running forever. In particular, we assume that strategies do not fail with exceptions. This is not a significant limitation. You can always replace a function f of type A => Option[B] that might throw an exception with the function x => Try(f(x)).getOrElse(None), which returns None instead.
- For a given input, all the strategies that produce a successful value produce the same value. (In my original context, if a theorem prover can show that a formula is valid, other provers cannot show that it is not, and vice versa.) There is no notion of “better” value. This makes it possible—and even desirable—to ignore the output of all the other strategies once a strategy has terminated successfully.
- Tasks are canceled by invoking their cancel method, which is customized for each strategy. This makes it easier for strategies to use code that is not responsive to thread interrupts—the default cancellation mechanism used by Java thread pools—such as socket I/O. (My verification tool ran theorem provers on remote computers.)
- Cancellation may be implemented on a “best effort” basis: A task may continue to run for some time after it has been canceled. Calling cancel on a task does not guarantee that a thread inside its run method completes this call immediately.
- Canceling a task before it runs prevents this task from ever running; if invoked, its run method returns None immediately. Canceling a task that is already finished has no effect.

For reference, a simple sequential implementation would try all the strategies in turn until either one produces a non-empty option or all the strategies have been exhausted:

```scala
{runner-seq}
class Runner[A, B](strategies: Seq[Strategy[A, B]]):
  def compute(input: A): Option[B] =
    strategies.view.flatMap(strategy => strategy(input).run()).headOption
```

A runner is created from a collection of strategies. Its compute method iterates over all the strategies, using a view. For each strategy, it creates and runs a task, until either one task produces a non-empty option or all the strategies fail. The use of a view guarantees that compute terminates as soon as a strategy is successful, without needlessly evaluating
