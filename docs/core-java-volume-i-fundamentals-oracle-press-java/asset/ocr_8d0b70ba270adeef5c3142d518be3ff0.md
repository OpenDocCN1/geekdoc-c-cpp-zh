removes the next completed result, blocking if no completed results are available.

+   - `Future<V> poll()`
+   - `Future<V> poll(long time, TimeUnit unit)`

removes and returns the next completed result, or returns `null` if no completed results are available. The second method waits for the given time.

# 12.6.4 The Fork-Join Framework

Some applications use a large number of threads that are mostly idle. An example would be a web server that uses one thread per connection. Other applications use one thread per processor core, in order to carry out computationally intensive tasks, such as image or video processing. The fork-join framework, which appeared in Java 7, is designed to support the latter. Suppose you have a processing task that naturally decomposes into subtasks, like this:

```
if (problemSize < threshold)
    solve problem directly
else
{
    break problem into subproblems
    recursively solve each subproblem
    combine the results
}
```

One example is image processing. To enhance an image, you can transform the top half and the bottom half. If you have enough idle processors, those operations can run in parallel. (You will need to do a bit of extra work along the strip that separates the two halves, but that’s a technical detail.)

Here, we discuss a simpler example. Suppose we want to count how many elements of an array fulfill a particular property. We cut the array in half, compute the counts of each half, and add them up.