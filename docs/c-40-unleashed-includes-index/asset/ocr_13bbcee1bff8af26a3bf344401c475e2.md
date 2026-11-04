```
```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    continueWith(a + b);
}
```
```

Notice we still have sequencing of operations going on: First, a and b are added together to be fed into the continuation function, which then runs after the addition takes place. Those operations are still sequential in nature. However, this is no longer the semicolon kind of sequencing we’re used to from languages such as C#. Now all the remaining code to execute after the addition sits in a lambda expression.

One essential difference that’s become visible after making this transformation is the change in Add’s return type. Now, the Add method returns void. It’s not that we have lost the result of the addition, though; the result will be fed to the continuation.

So far, we haven’t done anything truly different from the synchrony point of view. This code is still intrinsically synchronous: Calling Add computes the sum of its first two arguments, followed by a call to the continuation function. However, now we could easily introduce concurrency in the Add method to compute the sum of a and b without blocking the caller to Add. As soon as that value is available, the continuation function can be called, still on a different thread. In the world of CPS, the introduction of asynchrony becomes quite easy:

```
```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    new Thread(() => continueWith(a + b)).Start();
}
```
```

Now the Add method is an asynchronous method from the caller’s point of view. At the point this method returns, work is going on in the background without blocking the caller. When the sum value is available, the continuation will be called in the future.

# ### Hidden Continuations in the .NET Framework

Continuations have been prominent in the .NET Framework without them being called such. Probably the best example of them is the asynchronous method invocation pattern, which we can illustrate using BeginInvoke and EndInvoke on delegates:

```
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
```