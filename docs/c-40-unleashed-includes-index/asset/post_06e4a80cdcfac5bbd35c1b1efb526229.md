
Personally, I believe it's rather unlikely and superhuman if you can meaningfully recover from unhandled exceptions without knowing the bigger context of from where the error originates. If you think you can, this event might prove useful, though.

## Continuations

### The Basic Concept

Although they sound scary, continuations are really simple constructs. Before going into the specifics of their use in conjunction with tasks, let’s explore them from a conceptual point of view. Consider the following piece of imperative sequential synchronous code:

```csharp
int c = Add(a, b);
Console.WriteLine(c);
```

This piece of code calls a method Add, which at some point returns the sum of a and b, which we receive and can use to continue to use (for example, to print it to the screen). Let’s examine a few things about this code.

First, notice how sequencing plays an important role in the code: The call to the Console.WriteLine method cannot take place until Add returns. The semicolon syntax in languages such as C# makes the sequential execution nature explicit syntactically.

Second, and related to the previous point, this code is inherently synchronous: You can’t do anything but sit and wait for Add to come back before other work can be done. Although this seems tied to the notion of sequencing, we can still have sequencing without being synchronous. This is where continuations come in.

In continuation passing style (CPS), the preceding code fragment is rewritten in the following style, which at first might look a little weird:

```csharp
Add(a, b, c => {
    Console.WriteLine(c);
});
```

Now we call some method Add, which not only takes in its two inputs, it also accepts a callback parameter that receives the result of the computation. This is where execution continues after Add’s computation finishes (and hence the name continuation). Here’s how the Add method is implemented:

```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    continueWith(a + b);
}
```

Notice we still have sequencing of operations going on: First, a and b are added together to be fed into the continuation function, which then runs after the addition takes place. Those operations are still sequential in nature. However, this is no longer the semicolon kind of sequencing we’re used to from languages such as C#. Now all the remaining code to execute after the addition sits in a lambda expression.

One essential difference that’s become visible after making this transformation is the change in Add’s return type. Now, the Add method returns void. It’s not that we have lost the result of the addition, though; the result will be fed to the continuation.

So far, we haven’t done anything truly different from the synchrony point of view. This code is still intrinsically synchronous: Calling Add computes the sum of its first two arguments, followed by a call to the continuation function. However, now we could easily introduce concurrency in the Add method to compute the sum of a and b without blocking the caller to Add. As soon as that value is available, the continuation function can be called, still on a different thread. In the world of CPS, the introduction of asynchrony becomes quite easy:

```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    new Thread(() => continueWith(a + b)).Start();
}
```

### Hidden Continuations in the .NET Framework

Continuations have been prominent in the .NET Framework without them being called such. Probably the best example of them is the asynchronous method invocation pattern, which we can illustrate using BeginInvoke and EndInvoke on delegates:

```csharp
Func<int, int, int> add = (a, b) => a + b;
add.BeginInvoke(3, 4, iar =>
{
    int c = add.EndInvoke(iar);
    Console.WriteLine(c);
}, /* state */ null);

// The main thread can continue asynchronously while the delegate is being
// invoked. At some point the AsyncCallback continuation will be called.
```

If there’s just a single continuation, as shown in the preceding section’s example, it’s quite common to use a fluent interface pattern of dotting sequenced continuations together as a long chain:

```csharp
Task<int>.Factory.StartNew(() => 42)
.ContinueWith(t => t.Result / 2)
.ContinueWith(t => t.Result.ToString())
.ContinueWith(t => Console.WriteLine("42 / 2 = " + t.Result));
```

This works nicely if you put all error-handling or cancellation-handling logic inside the continuation functions. However, if you want to take distinct continuation actions for the different states a task can complete in, you must use the first style of assigning tasks to temporary variables to specify multiple continuations. Those two styles are contrasted in Figure 30.5.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1550_0.png)

FIGURE 30.5 Sequencing versus parallel continuations.

So here are some of the continuation option flags that can be specified when creating a new continuation:

- NotOn* flags prevent the continuation from running if the specified state is true for the antecedent task. Suffixes for this family of flags include Faulted, Canceled, and RanToCompletion.
- OnlyOn* flags, for the same three states as specified in the previous bullet point, cause the continuation to be called only if the antecedent task finished in the specified state.
- ExecuteSynchronously causes the continuation to run synchronously on the thread where the antecedent task completed. This option should be used only when the continuation is short running.

Other continuation options are the same as for the TaskCreationOptions, allowing for the specification of fairness preference, the long-running hint, or to attach the task to its parent.

An example of a task with two continuations, one for success and one for failure, is shown in the following code fragment:

```csharp
var answer = Task<int>.Factory.StartNew(() => {
    // Left to the reader: Compute a value "res"; may throw.
    return res;
});

answer.ContinueWith(t => {
    // Will only be called in success cases.
    Console.WriteLine(t.Result);
}, TaskContinuationOptions.OnlyOnRanToCompletion);

answer.ContinueWith(t => {
    // Will only be called in error cases. Handle any exception we can handle.
    t.Exception.Flatten().Handle(ex => {
        // See section "Exploring AggregateException" for more information.
        return false;
    });
}, TaskContinuationOptions.OnlyOnFaulted);
```

## THE FUTURE OF C# (AND VISUAL BASIC)

One feature that's most likely going to end up in a future release of C# is support for writing sequential-looking imperative-style asynchronous code. Continuations on tasks form the low-level machinery that allows chaining together asynchronous calls. Due to their low-level nature based on callbacks, code tends to be turned inside out, ending up in continuation lambdas with lots of error-checking code.

The new proposed async feature in C# 5.0 and VB 11.0 allows writing imperative-looking code based on a new expression called await:

```csharp
public async Task<int> CountWords(string url)
{
    string text = await DownloadStringAsync(url);
    return text.Split().Length;
}
```

Here, the DownloadStringAsync method is assumed to return a Task<string>. By performing an await operation on this task, the compiler turns the remainder code in the method into a continuation on this task. This just shows the tip of the iceberg of what's possible: All imperative constructs, such as branching and loops, can be used in an asynchronous method. Under the hood, the compiler generates a state machine of continuations, much like iterators do in C# 2.0 and later.

For more information, search the Web for "Visual Studio Async CTP"

In summary, continuations are used to chain together asynchronous computations. As discussed in the next section, it's also possible to cancel continuations. Given this option, and the ability to handle exceptions, continuations provide for sequencing points in chains of asynchronous computations.
