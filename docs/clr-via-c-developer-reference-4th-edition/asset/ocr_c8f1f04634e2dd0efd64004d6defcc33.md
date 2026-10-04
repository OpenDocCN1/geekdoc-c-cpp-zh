This code demonstrates another C# feature: async lambda expressions. You see, you can't just put an await operator inside the body of a regular lambda expression, because the compiler will know how to turn the method into a state machine. By placing async just before the lambda expression causes the state machine that returns a Task or Task<TResult>, which can then be assigned to any Func delegate whose return type is Task or Task<TResult>.

When writing code, it is very easy to invoke an async function, forgetting to use the await operator; the following code demonstrates:

```
static async Task OuterAsyncFunction() {
    // Oops, forgot to put the await operator on this line!

    // Code continues to execute while InnerAsyncFunction also continues to execute...
}
```

```
static async Task InnerAsyncFunction() { /* Code here is not important */ }
```

Fortunately, when you do this, the C# compiler gives the following warning: Because this call is not awaited, execution of the current method continues before the call is completed. Consider applying the 'await' operator to the result of the call. This is nice on rare occasions, when you don't actually care when InnerAsyncFunction completes, and you want to avoid writing the code and not have the compiler issue a warning.

To quiet the warning, you can simply assign the Task returned from InnerAsyncFunction to a variable and then ignore it.

```
static async Task OuterAsyncFunction() {
    var noWarning = InnerAsyncFunction(); // I intend not to put the await operator on this line.

    // Code continues to execute while InnerAsyncFunction also continues to execute...
}
```

Or, I prefer to define an extension method that looks like this.

```
[MethodImpl](MethodOptions.Aggressivelining)] // Causes compiler to optimize the call away
public static void NoWarning(this Task task) { /* No code goes in here */ }
```

And then can use it like this.

```
static async Task OuterAsyncFunction() {
    InnerAsyncFunction().NoWarning(); // I intend not to put the await operator on this line.

    // Code continues to execute while InnerAsyncFunction also continues to execute...
}
```

One of the truly great features of performing asynchronous I/O operations is that you can initiate many of them concurrently so that they are all executing in parallel. This can give your application

> Fortunately, the compiler does not give a warning about the local variable being used.