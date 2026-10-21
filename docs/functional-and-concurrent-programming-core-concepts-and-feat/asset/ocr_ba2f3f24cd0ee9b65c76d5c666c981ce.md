account. This design is based on the assumption that failed strategy runs might have succeeded with more time, but not with less.⁷ As before, the cache is organized as a thread-safe mapping from inputs to futures of outputs (see the rationale in Section 25.6) but also stores a timeout value associated with each future.

When a thread calls `compute` with an input value and a timeout, the mapping is searched for the input, and the outcome of this search is handled as follows:

+   1. *The input is not found.* In this case, the design from Listing 25.7 is reused: Put a promise into the mapping, and invoke strategies to complete it.
+   2. *A completed future with a value other than None is found.* This implies that a strategy was successful in the past. The desired output is taken from the future, and no further computation is necessary.
+   3. *A future is found but has no usable output.* This is either an incomplete future or a future completed with None. In this situation, there are two cases to consider:

+   (a) If the timeout associated with this earlier computation is larger than the timeout now specified, you have no hope of improving the result, due to the assumption stated earlier; don’t start a new computation, and use the future from the mapping.
+   (b) If the future in the mapping corresponds to a computation with a smaller timeout, you could use it in hopes that it produces a successful outcome, but there is also a chance that it has failed (or will fail) where a lengthier computation would have succeeded.

This is the interesting case. If the cached future is completed (with None), you can ignore it. But if it is still running, you need to consider it: It may soon produce a successful output. However, you cannot commit to it because it may still fail. Furthermore, the future can also switch from incomplete to complete at any moment while you are considering it.

You handle this case by initiating a new computation, with a larger timeout, and by using the first successful result available, either from this new computation or from the future already in the cache. Note that this approach works whether the cached future is completed or not, so it correctly handles the case where the cached future suddenly finishes in the middle of these steps, successfully or not.

Using Scala futures for a change—Listing 25.7 uses CompletableFuture—a possible implementation is as follows:

```
Scala
class Runner[A, B](strategies: Seq[Strategy[A, B]], exec: ExecutionContext)
    (using ScheduledExecutorService)(using ExecutionContext):
```

⁷This may not be true in practice, as computing resources may fluctuate, making it possible for shorter runs to use more actual CPU time than longer runs did.