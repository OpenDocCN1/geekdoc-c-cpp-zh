# Chapter 20: Programming the Task-Based Asynchronous Pattern

Similarly, the same effect can be achieved with a local function.15 For example, in Listing 20.10, you could change the lambda expression header (everything up to and including the => operator) to

```
async Task WriteWebRequestAsync(string webRequestUrl)
```

leaving everything in the body, including the curly braces, unchanged. Note that an async lambda expression has the same restrictions as named async method:

+   - An async lambda expression must be converted to a delegate whose return type is a valid async return type.
- The lambda is rewritten so that return statements become signals that the task returned by the lambda has completed with the given result.
- Execution within the lambda expression occurs synchronously until the first await on an incomplete awaitable is executed.
- All instructions following the await will execute as continuations on the return from the invoked asynchronous method (or, if the awaitable is already complete, simply will be executed synchronously rather than as continuations).
- An async lambda expression can be invoked with an await operator (shown in Listing 20.10).

# ADVANCED/BEGINNER TOP

Implementing a Custom Asynchronous Method
Implementing an asynchronous method by relying on other asynchronous methods (which, in turn, rely on more asynchronous methods) is relatively easy with the await keyword. However, at some point in the call hierarchy, it becomes necessary to write a "leaf" asynchronous Task-returning method. Consider, for example, an asynchronous method for running a command-line program with the eventual goal that the output could be accessed. Such a method would be declared as follows:

> 15. Starting in C# 7.0.