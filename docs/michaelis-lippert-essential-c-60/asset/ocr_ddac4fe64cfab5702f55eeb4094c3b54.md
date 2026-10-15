# ADVANCED TOPIC

# Cleaning up Following Iteration

Given that the classes that implement the IEnumerator<T> interface maintain the state, sometimes you need to clean up the state after it exits the loop (because either all iterations have completed or an exception is thrown). To achieve this, the IEnumerator<T> interface derives from IDisposable. Enumerators that implement IEnumerator do not necessarily implement IDisposable, but if they do, Dispose() will be called as well. This enables the calling of Dispose() after the foreach loop exits. The C# equivalent of the final CIL code, therefore, looks like Listing 14.10.

# LISTING 14.10: Compiled Result of foreach on Collections

```
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
System.Collections.Generic.Stack<int>.Enumerator
enumerator;
IDisposable disposable;

enumerator = stack.GetEnumerator();
try
{
    int number;
    while (enumerator.MoveNext())
    {
        number = enumerator.Current;
        Console.WriteLine(number);
    }
}
finally
{
    // Explicit cast used for IEnumerator<T>.
    disposable = (IDisposable) enumerator;
    disposable.Dispose();

    // IEnumerator will use the as operator unless IDisposable
    // support is known at compile time.
    // disposable = (enumerator as IDisposable);
    // if (disposable != null)
    // {
    //     disposable.Dispose();
    // }
}
```

Notice that because the IDisposable interface is supported by IEnumerator<T>, the using statement can simplify the code in Listing 14.10 to that shown in Listing 14.11.