
Notice how the TPL is only a small building block of a bigger story. In our coverage of task and data parallelism in this chapter, we focus on the TPL but also PLINQ, which, strictly speaking, is a different component. Let's talk about the layering a bit more.

At the bottom of the diagram, you can see a number of threads that correspond to the processors (or cores) in the machine. The allocation of those threads follows the ideas pointed out before and illustrated in Figure 30.2. In other words, the framework tries its best to avoid introducing more concurrency than the machine can handle, but also tries to provide as much concurrency as is tolerable. Obviously, the introduction of concurrency is primarily triggered by components higher up the stack requesting more computation resources.

One level higher up, we find two parallel components: the Task Parallel Library and the Data Structures for Coordination. The former of those is where the notion of tasks is defined. We detail this concept in a moment, but for now simply think of a task as a unit of work that can be run in parallel with other such tasks. The latter of the two embodies all sorts of data structures used in a parallel computing context. This ranges from concurrency-safe collection types in `System.Collections.Concurrent` to synchronization primitives, some of which were discussed in Chapter 29. We don't go into detail on those data structures here. In what follows, we abbreviate this component as CDS to stand for coordination data structures.

The bottom layers of the architecture form a fabric for computation on which a lot of applications can build. This is illustrated in the diagram by the arrow denoted with the word *Algorithms*. Any application can use the publicly exposed application programming interfaces (APIs) to do parallel programming, no matter what .NET language the developer prefers. However, it turns out the parallel programming libraries in .NET 4 can make direct use of the TPL and CDS. One prominent example is the PLINQ Execution Engine, which allows LINQ to Objects (and hence LINQ to XML) queries to be parallelized in an easy declarative manner. We look briefly at PLINQ, assuming prior knowledge of LINQ gained earlier in this book.

### Declarative Versus Imperative

An important aspect to point out about parallel programming is the way you express your intent in code. Historically, parallel programming has been mostly in the ballpark of an imperative approach. Most popular languages have imperative roots, including the C# language, which derives from C and C++. In those languages, you basically have to hold the hand of the machine and state explicitly what you want it to do.

Imperative languages are all about how you want things to be carried out. Essentially, you're sitting pretty close to the bare metal of the machine, manipulating instruction pointers through control flow, manipulating memory through assignment, and so on. As a result, there's little the machine, some runtime, or a language compiler can do to magically improve your code. There's little room to wiggle with the code you wrote. For example, consider the following loop:

```
foreach (var x in xs)
    ProcessItem(x);
```

Agreed, a smart compiler will do its best to make the loop go as efficiently as possible, but it won't violate some essential assumptions of the programming language in which you've written this code. One such assumption has a small syntactical footprint in the code, but has far-reaching implications. What I'm talking about is the single semicolon inside the loop body. You should read this innocent token in the code as sequencing. Boiling this down to its very essence, look at the following code:

```
A();
B();
```

All this means is to call A, and then call B. Similarly, for the foreach loop shown just a moment ago, the assumption is that ProcessItem is called for the elements of the sequence in the order over which they are iterated. That is, there's no room for parallel evaluation here.

## FUNDAMENTALIST FUNCTIONAL PROGRAMMING

One reason automatic parallelization of code is a red herring in today's programming languages and runtimes is the lack of “purity.” Side-effects pop up around every corner in programs, including the slightest bits of I/O. Let's illustrate this with an innocent example:

```
var now = new Tuple<DateTime, DateTime>(DateTime.Now, DateTime.Now);
```

Here, we create a tuple with both components set to the same DateTime.Now value. Or not? Reading the clock is an I/O operation that costs time, too. Hence, between evaluating the first DateTime.Now call and evaluating the second one, time will have elapsed. Both components of the tuple won't be the same!

Optimizing this code to eliminate the duplicate evaluation of DateTime.Now will produce different results. Now the two components of the tuple will always be the same. Because of the change in the code's semantics, such optimizations simply cannot be made. Even evaluating both DateTime.Now expressions in parallel is a big no-no. What if the two evaluations run on different processors, really at the same time? (Remember, clocks do have limited precision.)

As can be seen from the example shown here, imperative programming ties together the hands of the compiler, runtime, and machine, disallowing it from making certain optimizations. Although this can be said to be a contrived scenario, just imagine what would happen if DateTime.Now were not just about input but also about output. Any optimization would eliminate the duplicate output operation. Unfortunately, this also leaves out any room for legitimate safe optimizations. An example of such code is shown next:

```
var zeroes = new Tuple<double, double>(Math.Sin(0), Math.Sin(0));
```

The sine of zero isn't going to change. Now we could perfectly eliminate the common Math.Sin(0) subexpression and prevent wasting computation time, but there's nothing telling the compiler or the runtime this is okay to do.

In the world of fundamentalist pure functional programming, all side effects must be made explicit in types using so-called monads. As a result, evaluation order of a side effect-free portion of code can be done in any way the compiler or runtime sees fit. Imperative languages still have to learn a lot.

In a declarative world, things are quite different. In such a world, you just state what you want the code to produce as a result. The way the language, runtime, libraries, and ultimately the machine make this happen is irrelevant to you. All you care about are the results to be produced by the code. LINQ queries are a perfect example of declarative constructs:

```
var xs = Enumerable.Range(0, 1000);
var res = from x in xs
    where x % 2 == 0
    select x + 1;
```

```
foreach (var x in res)
    Console.WriteLine(x);
```

Nothing here prevents the query processor from splitting up the input sequence xs into multiple portions to run the filtering and projection code in parallel over them, merging results afterward. It turns out this is an almost true statement because you have to decorate the query with a little hint to make it run in parallel using PLINQ. We discussed this in Chapter 20, “Language Integrated Query Internals,” in the section, “Parallel LINQ.”

Parallel APIs in .NET 4 facilitate both ways of writing parallel programs. Primitives provided by the TPL are closer to imperative programming, whereas frameworks like PLINQ definitely are far more declarative. Some constructs are in the center of both approaches, making imperative constructs a bit more declarative. For example:

```
Parallel.ForEach(xs, x =>
    ProcessItem(x)
);
```

In this piece of code, we’re still writing what looks like an imperative foreach loop, but now we’re giving the framework a bit more flexibility. By using the Parallel class to formulate a foreach loop, we give the framework the freedom to run the loop body in parallel for each of the iterations. Notice the use of C# lambda expressions here, which make the code look as if there were a “parallel foreach” construct in the language.

## SYNCHRONIZE, SYNCHRONIZE, SYNCHRONIZE!

You might be tempted to sprinkle the parallel loop shown in our discussion all around your existing code base. Extreme caution should be taken, though. First, you don’t have any guarantee anymore about the order in which things will run. Because of this, results might appear in an order you don’t expect. For example, if the loop writes to a file or makes calls to a web service, those output operations will be shuffled around because of the parallel execution.

Second, our discussion about output-order complications pinpoints a potentially bigger problem. By now, whenever you hear the words input, output, or state mentioned in the same sentence as parallel or concurrent, a red flag should be raised. Our parallel foreach loop may run much faster, but why would you care if it no longer produces correct and safe results?

The important word is synchronization once more. Constructs introduced in .NET 4’s parallel programming libraries don’t have a crystal ball that allows them to inspect your code and see it’s thread safe. Proper synchronization continues to be your responsibility.

## What Are Tasks?

You can think about tasks in a variety of ways. One is to start from the notion of a thread and state that tasks are like lightweight threads, running on top of a pool of low-level operating system threads. This is quite an implementation-oriented definition that starts from machine-level mechanics and builds an abstraction out of it.

A better way to think about tasks is to see them as representations of future values that get computed by means of a function. As such, tasks are sources of asynchrony in your code: While the task is running, you can do other useful work, until the point you want to await the task’s result. Furthermore, tasks can be composed in a variety of ways.

In the definition in the preceding paragraph, the word future is used intentionally: Computer science literature often refers to this mechanism as futures (“in the future, there will be a value”) or promises (“the tasks promise to compute a value”). Contrast the data-oriented nature of tasks with regular threads to see the difference:

```
// Using threads, there's no convenient way to return data.
var a = 42;
new Thread(() => {
    var res = ComputeResult(a); // Using a closure, see Chapter 17, 'Delegates'
    // How can we return res?
}).Start();
```
