+   - Faulted The task terminated because of an exception.

In the next exercise, you'll report the status of each task so that you can see when they have completed or have been canceled.

# Canceling a Parallel For or Each loop

The `Parallel.For` and `Parallel.ForEach` methods don't provide you with direct access to the `Task` objects that have been created. The .NET runtime uses its own heuristics to determine the optimal number to use based on the resources available and the current workload of the computer.

If you want to stop the `Parallel.For` or `Parallel.ForEach` method early, you must use a `Parallel-LoopState` object. The method you specify the body of the loop includes an additional `ParallelLoopState` parameter. The `Parallel` class creates a `ParallelLoopState` object and passes it into the method. The `Parallel` class uses this object to hold information about each invocation. The method can call the `Stop` method of this object to indicate that the `Parallel` class should not attempt to perform any iterations that have already started and finished.

The example that follows shows the `Parallel.For` method calling the `doLoopWork` method for each iteration. The `doLoopWork` method examines the iteration variable. If it is greater than `600`, the method calls the `Stop` method of the `ParallelLoopState` parameter. This causes the `Parallel.For` method to stop running further iterations of the loop. (Iterations currently might continue to completion.)

![](bbox=[0.163, 0.678, 0.26, 0.725])

Remember that the iterations in a `Parallel.For` loop are not run in a specific sequence. Consequently, canceling the loop when the iteration variable has the value `600` does not guarantee that the previous 599 iterations have already run. Likewise, some iterations with greater than 600 might already have completed.

Click here to view code image