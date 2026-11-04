# # LET MEASUREMENT BE YOUR GUIDE

It can't be emphasized enough that measurement should be the guide to carrying out optimizations. The first question to ask is whether the original code meets a certain min-bar with regard to execution time. If it doesn't, the next step is to look out for possible optimizations.

Quantitative analysis is the key to successful evaluation of performance, especially in core data processing tasks where the raw performance matters and is not directly subject to user perception. In the world of UI programming, you most likely want to carry out user-satisfaction studies to figure out whether your application is responsive enough.

One of the big benefits of PLINQ in particular, and the .NET 4 Task Parallel Library in general, is the ease by which you can simply try to parallelize a piece of code (for example, by sticking AsParallel on a query). In imperative programming, you'd be faced with a complete overhaul of the code. Sadly, people often cross the barrier of correctness when attempting to make their code run faster. The smallest mistake can have disastrous impact on the code's meaning, sometimes going unnoticed for a long time due to the nondeterminism of parallel code execution. With technologies such as PLINQ, the cost of trying out some parallelization is low, so evaluation of a certain optimization strategy is cheap.

# ## How PLINQ Works

We can approach the question of how PLINQ does its magic in two ways. We can look behind the scenes and study various techniques used to partition input sequences efficiently, to avoid locking when merging results together and to analyze the query wholesale to decide on certain parallelization strategies at runtime. Although all of this is incredibly interesting, we would need a whole book to cover all of this. Alternatively (and what we do here), we can ask ourselves how PLINQ gets a chance to analyze the query expression for various forms of optimization at runtime. This is immediately related to the query pattern we've seen before.

Let's start by repeating the exercise of decomposing a query expression, this time with an AsParallel call on one of its sources, into individual methods. The sample query shown earlier translates into the following:

```
var res = Enumerable.Range(0, 10000).AsParallel()
    .SelectMany(x => Enumerable.Range(0, 10000), (x, y) => new { x, y })
    .Where(_ => _.x > _.y)
    .Select(_ => _.x + _.y);
```

The precise mechanics of the SelectMany translation with transparent identifiers is irrelevant in this context. What matters more is the observation that AsParallel sits right in front of the subsequent query operator calls.

Because of this, the return type of the AsParallel call will be essential in the further resolution of the query operator methods following it. If you go to the definition of this