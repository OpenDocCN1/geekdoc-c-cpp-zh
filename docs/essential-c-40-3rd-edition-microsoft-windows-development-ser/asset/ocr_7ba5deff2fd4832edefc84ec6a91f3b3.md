iterations. In the context of parallel for execution, however, break identifies that no new iterations following the breaking iteration should start. All currently executing iterations will run to completion.

For example, given the following circumstances:

+   • A total of ten iterations numbered sequentially from 1 to 10

+   • Iteration 7 has run to completion

+   • Iterations 3, 5, 7, and 9 are currently executing (remember, the order of execution is determined by the task scheduler and is not necessarily sequential)

+   • A break (ParallelLoopState.Break()) executes on iterations 5 and 7 at the conclusion of the parallel loop, iterations 1 through 5 7, and 9 will complete. Iterations 6 and 8 will not complete (they never even started before 5 was canceled).

To determine the lowest iteration to execute a break and identify whether the break prevented one or more iterations from starting, the parallel For()/ForEach() method returns a System.Threading.ParallelLoopResult object. This result object has the following properties:

+   • IsCompleted: returns a Boolean indicating whether all iterations started.

+   • LowestBreakIteration: identifies the lowest iteration that executed a break. The value is of type long?, where a value of null indicates no break statement was encountered.

Returning to the ten-iteration example, the IsCompleted property will return false and the LowestBreakIteration will return a value of 5. The C# break statement equivalent is possible using the ParallelLoopState.Break() method where the ParallelLoopState is a type parameter on the Action<int, ParallelLoopState> specified in some of the parallel For()/ForEach() loop overloads.

In addition to ParallelLoopState.Break() there is also a ParallelLoopState.Stop(). The behavior is similar to break except that iterations that have not yet started, even those prior to the iteration executing the