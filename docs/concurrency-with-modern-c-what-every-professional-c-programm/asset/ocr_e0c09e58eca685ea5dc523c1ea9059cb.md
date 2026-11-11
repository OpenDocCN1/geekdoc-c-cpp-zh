# **An executor from an executor adaptor**

```
~~~cpp
// get an executor from a thread pool
auto exec = pool_executor();

// wrap the thread pool's executor in a logging_executor
logging_executor<decltype(exec)> logging_exec(exec);

// use the logging executor in a parallel sort
std::sort(std::execution::par_on(logging_exec), my_data.begin(), my_data.end());
~~~
```

logging_executor is in the code snippet a wrapper for the pool executor.

# ### 7.1.4 Goals of an Executor Concept

What are the goals of an executor concept according to the proposal P1055¹⁹?

+   1. **Batchable**: control the trade-off between the cost of the callable transition and its size.
+   2. **Heterogenous**: allow the callable to run on heterogeneous contexts and get the result back.
+   3. **Orderable**: specify the order in which the callables are invoked. The goal includes ordering guarantees such as LIFO²⁰ (Last In, First Out), FIFO²¹ (First In, First Out) execution, priority or time constraints, or even sequential execution.
+   4. **Controllable**: the callable has to be targetable to a specific computing resource, deferred, or even canceled.
+   5. **Continuable**: to control asynchronous callable signals are needed. These signals have to indicate whether the result is available, whether an error occurred, when the callable is done or if the callee wants to cancel the callable. The explicit starting of the callable or the stopping of the starting callable should also be possible.
+   6. **Layerable**: hierarchies allow capabilities to be added without increasing the simpler use-cases' complexity.
+   7. **Usable**: ease of use for the implementer and the user should be the primary goal.
+   8. **Composable**: allows a user to extend the executors for features that are not part of the standard.
+   9. **Minimal**: nothing should exist on the executor concepts that could be added externally in a library on top of the concept.

+   19. https://open-std.org/JTC1/SC22/WG21/docs/papers/2018/p1055r0.pdf
+   20. https://en.wikipedia.org/wiki/Stack_(abstract_data_type)
+   21. https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)