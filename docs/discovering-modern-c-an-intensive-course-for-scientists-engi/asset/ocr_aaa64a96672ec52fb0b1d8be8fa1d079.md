# 4.6 Concurrency

Every general-purpose processor sold these days contains multiple cores. However, exploring the compute power of multi-core platforms is still a challenge for many programmers. In addition to keeping several cores busy, multi-threading can also be useful on a single core for using it more efficiently, e.g., loading data from the web while the received data is processed. Finding the right abstractions to provide maximal clarity and expressiveness on one hand and optimal performance on the other is one of the most important challenges of the C++ evolution.

The first concurrent features were introduced in C++11. Currently, the fundamental components of concurrent programming are:

+   - thread: class for a new path of execution;
+   - async: calls a function asynchronously;
+   - atomic: class template for non-interleaved value access;
+   - mutex: facility to steer mutually exclusive execution;
+   - future: class template to receive a result from a thread; and
+   - promise: template to store values for a future.

As a use case, we want to implement an asynchronous and interruptible iterative solver. Such a solver will offer the scientist or engineer more productivity:

+   - Asynchrony: We can already work on the next model while the solver is running.
+   - Interruptibility: If we are convinced that our new model is much better, we can as well stop the solution of the old model.

Unfortunately, a thread cannot be killed. Well, it can but this aborts the entire application. To stop threads properly, they must cooperate by supplying well-defined interruption points. The most natural occasion to stop an iterative solver is in the termination test at the end of each iteration. This doesn't allow us to stop the solver immediately. For typical real-world applications where very many reasonably short iterations are performed, this approach offers a good benefit for relatively little work.

Thus, the first step toward an interruptible solver is an interruptible iteration control class. For the sake of brevity, we build our control class on top of `basic_iteration` from MTL4 [17], and we apologize that the complete code for this example is not publicly available. An iteration object is initialized with an absolute and relative epsilon plus a maximal number of iterations—or a subset thereof. An iterative solver computes after each iteration a certain error estimation, typically a norm of the residuum—and checks with the iteration control object whether the calculation should be finished. Our job is now to incorporate there a test for possibly submitted interruptions:

```
class interruptible_iteration
{
    public:
```