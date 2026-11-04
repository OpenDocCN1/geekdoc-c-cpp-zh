should be included in the resulting sequence. And that's precisely what happens in the `if` statement. If the predicate says yes, the element is yielded to the caller. And all of this is done in a lazy fashion: When the caller stops pulling out elements from the query, no more elements are analyzed, and the loop terminates. Fascinating, isn't it?

LINQ enables us to arbitrarily chain together several operators. For filtering, `Where` is used; it takes in a sequence and produces a new one. In our sample query, we fed the output of this filtering operation into the projection done by `Select`, producing yet another sequence. And we can continue doing so, with operations like sorting, grouping, aggregation, and so on. This concept is illustrated graphically in Figure 7.22.

![](bbox=[0.073, 0.375, 0.945, 0.69])

FIGURE 7.22 Interaction between different iterators in a query.

This use of wheels and chains precisely illustrates the point. The `foreach` statement essentially pulls the chain, causing the `Select` wheel to move. Internally, this one uses a `foreach` statement to suck data out of the results of the `Where` query operator. And that one ultimately consumes data from the data source; in our case, `Process.GetProcesses()`. As soon as the consuming `foreach` statement stops running (for example, because of a `break` statement), the iterators connected through the chain stop ticking, too.

We discuss LINQ in much more detail later on, but I want you to remember one thing right now. If you're writing loop constructs to process data, LINQ might be a better choice. For one thing, it leads to a dramatic improvement in code readability, and laziness can be an advantage to avoid needless computation.