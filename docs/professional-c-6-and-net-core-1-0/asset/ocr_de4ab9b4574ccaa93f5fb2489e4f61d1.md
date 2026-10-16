```
WriteLine($"lowest break iteration:
{result.LowestBreakIteration}");
}
```

This run of the application demonstrates that the iteration breaks up with a value higher than 12, but other tasks can simultaneously run, and tasks with other values can run. All the tasks that have been started before the break can continue to the end. You can use the LowestBreakIteration property to ignore results from tasks that you do not need:

```
S 31, task: 6, thread: 8
S 17, task: 7, thread: 5
S 10, task: 5, thread: 1
S 24, task: 8, thread: 6
break now 24, task: 8, thread: 6
S 38, task: 9, thread: 7
break now 38, task: 9, thread: 7
break now 31, task: 6, thread: 8
break now 17, task: 7, thread: 5
E 17, task: 7, thread: 5
E 10, task: 5, thread: 1
S 11, task: 5, thread: 1
E 38, task: 9, thread: 7
E 24, task: 8, thread: 6
E 31, task: 6, thread: 8
E 11, task: 5, thread: 1
S 12, task: 5, thread: 1
E 12, task: 5, thread: 1
S 13, task: 5, thread: 1
break now 13, task: 5, thread: 1
E 13, task: 5, thread: 1
Is completed: False
lowest break iteration: 13
```

# Parallel For Initialization

Parallel.For might use several threads to do the loops. If you need an initialization that should be done with every thread, you can use the Parallel.For<TLocal> method. The generic version of the For method accepts—in addition to the from and to values—three delegate parameters. The first parameter is of type Func<TLocal>. Because the example here uses a string for TLocal, the method needs to be defined as Func<string>, a method returning a string. This method is invoked only once for each thread that is used to do the iterations.

The second delegate parameter defines the delegate for the body. In the example, the parameter is of type Func<int, ParallelLoopState, string, string>. The first parameter is the loop iteration; the second parameter, ParallelLoopState, enables stopping the loop, as shown earlier. With the third parameter, the body method receives the value that is returned from the init method. The body method also needs to return a value of the type that was defined with the generic For parameter.

The last parameter of the For method specifies a delegate, Action<TLocal>; in the example, a string is received. This method, a