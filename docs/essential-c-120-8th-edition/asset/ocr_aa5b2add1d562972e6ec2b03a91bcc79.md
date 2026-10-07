which adding more threads begins making performance worse. Once that point is reached, the number of threads can then be decreased back to the number that produced the best performance.

The TPL does not associate top-level tasks that are waiting to be executed with any particular thread. If, however, a task running on a thread itself creates another task, the newly created task is associated with that thread automatically. When the new child task is eventually scheduled to run, it usually runs on the same thread as the task that created it. The work-stealing algorithm identifies threads that have an unusually large or unusually amount of pending work; a thread that has too few tasks associated with it sometimes "steal" not-yet-executed tasks from threads that have too many tasks waiting to run.

The key feature of these algorithms is that they enable the TPL to dynamically tune its own performance to mitigate overscheduling and underscheduling and balance the work among the available processors.

The TPL generally does a good job of tuning its performance, but can help it do a better job by providing hints the best course of action. Specifying the TPL TaskCreationOptions.LongRunning option described in the section "Long-Running Tasks" in Chapter 19 is an example of such a hint. You can also explicitly tell the task scheduler how many threads you think would be best to service a parallel loop; see "Advanced Topic: Parallel Loop Options" later in this chapter for more details.

# BEGINNER TOPIC

# Parallel Loop Exception Handling with AggregateException

The TPL catches and saves exceptions associated with tasks in an AggregateException, because a given task may have several exceptions obtained from its subtasks. This is also the case with parallel execution of loops: Each iteration could have produced an exception, so the exceptions need to be gathered into one aggregating exception. Consider the example in Listing 21.4 and its results in Output 21.2.