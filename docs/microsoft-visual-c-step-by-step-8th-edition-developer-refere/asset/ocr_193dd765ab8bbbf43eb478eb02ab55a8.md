```
}
...
```

Similarly, you can specify the value *TaskContinuationOptions.OnlyOnFaulted* to specify a continuation that runs if the original method run by the task raises an unhandled exception.

# Summary

In this chapter, you learned why it is important to write applications that can scale across multiple processors and processor cores. You saw how to use the Task class to run operations in parallel and how to synchronize concurrent operations and wait for them to complete. You learned how to use the *Parallel* class to parallelize some common programming constructs, and you also saw when it is inappropriate to parallelize code. You used tasks and threads together in a graphical user interface to improve responsiveness and throughput, and you saw how to cancel tasks in a clean and controlled manner.

+   - If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to [Chapter 24](Chapter 24).
+   - If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

# Quick reference