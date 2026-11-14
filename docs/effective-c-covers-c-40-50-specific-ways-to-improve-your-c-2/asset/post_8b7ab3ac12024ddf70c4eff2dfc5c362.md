
```
testing element: 11
testing element: 12
testing element: 13
testing element: 14
testing element: 15
testing element: 16
testing element: 17
testing element: 18
testing element: 19
testing element: 20
projecting an element: 20
called MoveNext
Delivered 20 at 1:46:08 PM
testing element: 21
testing element: 22
testing element: 23
testing element: 24
testing element: 25
testing element: 26
testing element: 27
testing element: 28
testing element: 29
testing element: 30
projecting an element: 30
```

The query does not begin to execute until the first call to MoveNext() on the enumerator. The first call to MoveNext() executes the query on enough elements to retrieve the first element on the result sequence (which happens to be one element for this query). The next call to MoveNext() processes elements in the input sequence until the next item in the output sequence has been produced. Using LINQ to Objects, each call to MoveNext() executes the query on as many elements are necessary to produce the next output element.

The rules change once you change the query to be a parallel query:

```
var answers = from n in ParallelEnumerable.Range(0, 300)
where n.SomeTest()
select n.SomeProjection();
```

The output from this query will look very different. Here's a sample from one run (it will change somewhat for each run):

About to start iterating
testing element: 150
projecting an element: 150
testing element: 0
projecting an element: 0
testing element: 1
testing element: 2
testing element: 3
testing element: 4
testing element: 5
testing element: 6
testing element: 7
testing element: 8
testing element: 9
testing element: 10
projecting an element: 10
testing element: 11
testing element: 12
testing element: 13
testing element: 14
testing element: 15
testing element: 16
testing element: 17
testing element: 18
testing element: 19
testing element: 152
testing element: 153
testing element: 154
testing element: 155
testing element: 156
testing element: 157
testing element: 20
... Lots more here elided ...
... testing element: 286
testing element: 287
testing element: 288
testing element: 289
testing element: 290
Delivered 130 at 1:50:39 PM

```
called MoveNext
Delivered 140 at 1:50:39 PM
projecting an element: 290
testing element: 291
testing element: 292
testing element: 293
testing element: 294
testing element: 295
testing element: 296
testing element: 297
testing element: 298
testing element: 299
called MoveNext
Delivered 150 at 1:50:39 PM
called MoveNext
Delivered 160 at 1:50:39 PM
called MoveNext
Delivered 170 at 1:50:39 PM
called MoveNext
Delivered 180 at 1:50:39 PM
called MoveNext
Delivered 190 at 1:50:39 PM
called MoveNext
Delivered 200 at 1:50:39 PM
called MoveNext
Delivered 210 at 1:50:39 PM
called MoveNext
Delivered 220 at 1:50:39 PM
called MoveNext
Delivered 230 at 1:50:39 PM
called MoveNext
Delivered 240 at 1:50:39 PM
called MoveNext
Delivered 250 at 1:50:39 PM
called MoveNext
Delivered 260 at 1:50:39 PM
called MoveNext
Delivered 270 at 1:50:39 PM
called MoveNext
Delivered 280 at 1:50:39 PM
```

called MoveNext

Delivered 290 at 1:50:39 PM

Notice how much it changed. The very first call to MoveNext() causes PLINQ to start all the threads involved in generating the results. That causes quite a few (in this case, almost all) result objects to be produced. Each subsequent call to MoveNext() will grab the next item from those already produced. You can predict when a particular input element will be processed. All you know is that the query will begin executing (on several threads) as soon as you ask for the first element of the query.

PLINQ's methods that support query syntax understand how this behavior can affect performance on queries. Suppose you modify the query to select the second page of results using Skip() and Take():

```
var answers = (from n in ParallelEnumerable.Range(0, 300)
               where n.SomeTest()
               select n.SomeProjection()).
               Skip(20).Take(20);
```

Executing this query produces output that is identical to that produced by LINQ to Objects. That's because PLINQ knows that it will be faster to produce only 20 elements rather than 300. (I'm simplifying, but PLINQ's implementation of Skip() and Take() do tend to favor a sequential algorithm more than other algorithms.)

You can modify the query a bit more, and get PLINQ to generate all the elements using the parallel execution model. Just add an orderby clause:

```
var answers = (from n in ParallelEnumerable.Range(0, 300)
               where n.SomeTest()
               orderby n.ToString().Length
               select n.SomeProjection()).
               Skip(20).Take(20);
```

The lambda argument for orderby must not be something that the compiler can optimize away (that's why I used n.ToString().Length rather than just n above). Now, the query engine must generate all the elements of the output sequence before it can order them properly. Only once the elements are ordered properly can the Skip() and Take() methods know which elements should be returned. Of course, it's faster on multicore machines to use multiple threads to generate all the output than it would be to generate the sequence sequentially. PLINQ knows that, too, so it starts multiple threads to create the output.

PLINQ tries to create the best implementation for the queries you write in order to generate the results you need with the least amount of work, and in the least amount of time. Sometimes that means PLINQ queries will execute in a different manner than you would expect. Sometimes it will act more like LINQ to Objects, where asking for the next item in the output sequence executes the code that produces it. Sometimes it will behave more like LINQ to SQL or Entity Framework in that asking for the first item will produce all of them. Sometimes it will behave like a mixture of the two. You should make sure that you don't introduce any side effects in your LINQ queries. Those will be unreliable in a PLINQ execution model. You should construct your queries with some care to ensure that you get the most out of the underlying technology. That requires you to understand how they work differently.

Parallel algorithms are limited by Amdahl's law: The speedup of a program using multiple processors is limited by the sequential fraction of the program. The extension methods in ParallelEnumerable are no exception to this rule. Many of these methods can operate in parallel, but some of them will affect the degree of parallelism due to their nature. Obviously OrderBy and ThenBy require some coordination between tasks. Skip, SkipWhile, Take, and TakeWhile will affect the degree of parallelism. Parallel tasks running on different cores may finish in different orders. You can use the AsOrdered() and AsUnordered() methods to instruct PLINQ as to whether or not order matters in the result sequence.

Sometimes your own algorithm relies on side effects and cannot be parallelized. You can force sequential execution using the ParallelEnumerable.AsSequential() extension method to interpret a parallel sequence as an IEnumerable and force sequential execution.

Finally, ParallelEnumerable contains methods that allow you to control how PLINQ executes parallel queries. You can use WithExecutionMode() to suggest parallel execution, even if that means selecting a high overhead algorithm. By default, PLINQ will parallelize those constructs where it expects parallelism to help. You can use WithDegreeOfParallelism() to suggest the number of threads that may be used in your algorithm. Usually, PLINQ will allocate threads based on the number of processors on the current machine. You can also use the WithMergeOptions() to request a change in how PLINQ controls buffering results during a query. Usually, PLINQ will buffer some results from each thread before making them available to the consumer thread. You can request no buffering to make results available immediately. You can request full buffering, which will increase performance at a cost of higher latency. Auto Buffering, the default, provides a balance between latency and performance. Buffering is a hint, not a demand. PLINQ may ignore your request.

I'm not providing any specific guidance on which of these settings is best for you because they will be highly dependent on your algorithm. However, you have those settings that you can change, and you should experiment on a variety of target machines to see if these will help your algorithms. If you don't have several different target machines to experiment with, I'd recommend using the defaults.

PLINQ makes parallel computing much easier than it previously was. It's an important time for these additions; parallel computing will continue to become more important as more and more cores become commonplace for desktop and laptop computers. It's still not easy. And poorly designed algorithms may not see performance improvements from parallelization. Your task is to look for loops and other tasks that can be parallelized. Take those algorithms and try the parallel versions. Measure the results. Work on the algorithms to get better results on the performance. Realize that some algorithms aren't easily parallelizable, and keep those serial.

## Item 36: Understand How to Use PLINQ for I/O Bound Operations

The Parallel Task Library looks like it would be optimized for CPU bound operations. While that is a core mission for the library, it does work well with I/O bound operations as well. In fact, the design of the Parallel Task Library handles I/O bound operations rather well by default. It will update the number of threads allocated to your algorithms based on the how busy those threads are. More blocked threads (waiting for I/O operations) will result in the ThreadPool allocating more threads to the tasks at hand.

As with other parallel extensions, you can use method calls, or LINQ query syntax to opt into a parallel execution model. Parallel execution for I/O bound operations behaves a little differently than CPU bound operations. You'll often want more threads than cores, because the I/O bound threads spend more of their time waiting for some external event. PLINQ provides a framework for these idioms as well.
