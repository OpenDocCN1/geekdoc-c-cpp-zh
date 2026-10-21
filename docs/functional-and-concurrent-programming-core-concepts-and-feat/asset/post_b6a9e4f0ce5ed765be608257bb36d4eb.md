
# Chapter 16 Concepts of Concurrent Programming

This program is sequential and prints A, B, and C, in that order. You can break sequentiality by letting the second print statement execute out of order. In Scala, it could be written as follows:

```
```scala
println('A')
Future(println('B'))
println('C')
```
```

The second print statement is scheduled to be executed out of order, and the program output is no longer guaranteed to be A followed by B followed by C. Out-of-order execution can also be triggered in other languages like Kotlin:

```
```kotlin
println('A')
launch { println('B') }
println('C')
```
```

or JavaScript:

```
```javascript
console.log('A');
Promise.resolve().then(() => console.log('B'));
console.log('C');
```
```

In the initial pseudocode, println('B') is a synchronous call: It takes place here and now, within the current run, between the printing of A and the printing of C. By contrast, the Scala line Future(println('B')), the Kotlin line launch { println('B') }, and the JavaScript line Promise.resolve().then(() => console.log('B')) have the similar effect of invoking the printing of B asynchronously, not here and/or not now, out of the current flow of operations.

As a noncomputing analogy, if I order a sandwich and stand at the counter while the sandwich is being prepared in front of me, that’s synchronous. If instead I place my order, get a number, and don’t wait for the sandwich to be ready before leaving the counter, that’s asynchronous.¹

So, the three programs just shown are no longer sequential. Are they concurrent?

The JavaScript program uses a single thread and guarantees that B will be printed after A and C, in an ACB order. The printing of B is not happening “now,” but in a way it is still happening “here,” within the same thread of execution. Given that the program is single-threaded, and that the ACB order is guaranteed, you can even argue that the execution is still sequential, only in a different order.

> In this case, it is also multithreaded, only in a different order. unless I’m being asked to make the sandwich myself when I come back to the counter to pick it up.

Is concurrency, then, tied to the use of multiple threads? Depending on how they are configured, the example Scala and Kotlin programs may or may not rely on an additional thread to execute the printing of B. Can the same program be concurrent or not, depending on external configuration? Even if we assume that the Scala and Kotlin programs are configured to use multiple threads when Future or launch is invoked, does that necessarily make them concurrent? Consider these variants:

```
println('A')
Await.ready(Future(println('B')), Duration.Inf)
println('C')
```

```
println('A')
launch { println('B') }.join()
println('C')
```

Because of added synchronization, these programs, even when they use multiple threads, will print A, B, and C, in the ABC order. You could say that the printing of B is not taking place “here,” in the current thread of execution, but it is still happening “now,” between A and C. Does this make the programs sequential, or are they still concurrent? Are there multithreaded sequential programs?² Furthermore, even in the earlier, non-synchronized versions of the programs, A, B, and C are bound to be printed in some order, one at a time, sequentially. It’s not as if two letters could end up on top of each other, or even on the same line. So, what is concurrent in these nominally non-sequential programs?

Let’s modify the Scala program to use a slow printing function:

```
def slowPrint(x: Any) =
  var n = BigInt("1000000000")
  while n > 0 do n -= 1
  println(x)
slowPrint('A')
Future(slowPrint('B'))
slowPrint('C')
```

Printing each letter now takes time because it requires counting down from a large number using big integers. Using a single-threaded configuration, on the multicore computer

> You might argue that these last two examples are silly and artificial (they are). But more realistic illustrations exist. For instance, the code that handles incoming messages in actors (Section 27.5) is typically executed sequentially by multiple threads, one at a time.

used for typesetting this book, the program takes 7.6 seconds to complete and prints the letters in the ACB order, like the JavaScript program. With a multithreaded configuration, the running time is reduced to 5.2 seconds, about two-thirds of the single-threaded time. This is because the slow printing of B and the slow printing of C are now running concurrently, inside two separate threads of execution. The time is reduced from

(printing of A) + (printing of B) + (printing of C)

to

(printing of A) + max((printing of B) + (printing of C))

Two of the computer’s cores perform the slow countdown at the same time, in parallel, even if the actual printing of the two letters on the terminal still happens sequentially, B before C or C before B. In other words, there is concurrency at the level of two cores executing big integer operations, but printing on a shared terminal remains sequential (as it should), even when multiple threads are involved.

## NOTE

At this point, you may expect the obligatory discussion of concurrency versus parallelism to take place. In books and Internet blogs, this is often considered to be a fundamental point to be addressed early on. I disagree. As definitive as the many explanations aim to be, they tend to be inconsistent with one another. If you corner me, as students have, and insist that I make a distinction, my view—inspired by the Association for Computing Machinery (ACM) Computer Science Curricula 2013—is that parallelism is the concurrency I want (for speed!), and concurrency is the parallelism I need to deal with (all those things happening at the same time in my program). However, my argument here is that it doesn’t matter much. By and large, you face the same programming challenges whether you attribute them to parallelism or to concurrency. For the purposes of this book, it is enough to stick with basic dictionary definitions and to think of parallelism and concurrency as synonymous, both representing the idea of several actions taking place at (about) the same time. In the following chapters, I use both terms interchangeably.

## 16.2 Concurrent Programming Concepts

The code snippets from Section 16.1 did not lead to a clear definition of what concurrency is, but they can still be used to illustrate several fundamental concepts of concurrent programming, explored in the following chapters.

- *Asynchronicity* is what triggers out-of-order execution. Concurrent programs involve asynchronous operations, which deviate from the simpler, sequential programs all developers are familiar with: `println('B')` prints B synchronously; `Future(println('B'))` does it asynchronously, whether it introduces parallelism or not. When writing concurrent programs, you need to take into consideration

- *Threads of execution*, or threads for short, are a common source of concurrency in programs, but they are not the only one: Processes tend to run concurrently as well, and external events such as user clicks or incoming server connections also introduce concurrency. Furthermore, programmers often handle concurrency at non-thread levels—for instance, in terms of tasks, or futures, or actors, or coroutines.
- *Atomicity* defines elementary program units, the “parts” that can be executed out of order, or “at the same time.” In the examples in Section 16.1, for instance, decrementing a BigInt by one is an atomic operation, but counting down from 1,000,000,000 to zero is not. Similarly, a letter is printed on the terminal, or it is not; it cannot be “partially printed.” In contrast, printing multiple letters is not necessarily atomic. The single-threaded JavaScript program guarantees that the A and C lines form an atomic unit, with no possible B in between, while the Scala and Kotlin programs—when configured to use multiple threads—do not. As a programmer, you must be aware of what needs to be atomic in your program and of the atomicity guarantees of the languages and libraries with which you are programming.
- *Synchronization* is often needed to coordinate concurrent activities. You can use *synchronizers*, such as locks and semaphores, to reduce the concurrency of a program to a level that does not jeopardize the program’s correctness. When synchronizers are misused—as I did earlier with Scala’s Await and Kotlin’s join—they can turn a concurrent program into a sequential one, or even prevent the program from running at all (see the discussion of deadlocks in Section 22.3).
- *Nondeterminism* is a natural consequence of concurrency and is the bane of concurrent programming. The most salient difference between the JavaScript program, on the one hand, and the Scala and Kotlin programs, on the other hand—when configured to be multithreaded, without additional synchronization—is that the former can produce the three letters in only one possible sequence, ACB, while the others may produce different sequences in different runs. The impact of such nondeterministic behaviors on testing and debugging is momentous.

## 16.3 Summary

There is no need to delve into a philosophical discussion of what constitutes concurrent programming to introduce several of the core concepts that underlie many programming language constructs, such as threads of executions, asynchronous calls, atomic actions, synchronization, and nondeterminism. The art of concurrent programming is to write programs that properly balance multiple facets of concurrency: Too many threads (or
