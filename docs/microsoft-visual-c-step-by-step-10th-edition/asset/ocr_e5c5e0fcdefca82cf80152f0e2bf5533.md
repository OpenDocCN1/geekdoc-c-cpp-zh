core, quad-core processor that all have the same clock frequency. The difference is that on a dual-core processor, as far as your application is concerned, one of the processor cores will be sitting around idle, and on a quad-core processor, three of the cores will be simply ticking away, waiting for work. To make the best use of multicore processors, you must write your applications to take advantage of multitasking.

# Implementing multitasking by using Microsoft .NET

Multitasking is the ability to do more than one thing at the same time. It is one of those concepts that's easy to describe but until recently has been difficult to implement.

In the optimal scenario, an application running on a multicore processor performs as many concurrent tasks as there are processor cores available, keeping each of the cores busy. However, to implement concurrency, you must consider many issues, including the following:

+   - How can you divide an application into a set of concurrent operations?

+   - How can you arrange for a set of operations to execute concurrently, multiple processors?

+   - How can you ensure that you perform only as many concurrent operations as there are processors available?

+   - If an operation is blocked (such as while waiting for I/O to complete), how can you detect this and arrange for the processor to run a different operation rather than sit idle?

+   - How can you determine when one or more concurrent operations have completed?

To an application developer, the first question is a matter of application design. The remaining questions depend on the programmatic infrastructure. Microsoft provides the Task class and a collection of associated types in the System.Threading.Tasks namespace to help address these issues.

> **Important
The point about application design is fundamental. If an application is not designed with multitasking in mind, then it doesn't matter how many