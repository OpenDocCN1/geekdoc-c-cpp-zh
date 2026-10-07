# What Makes a Class a Collection: IEnumerable

LISTING 15.6: A Separate Enumerator Maintaining State during an Iteration

```
System.Collections.Generic.Stack<int> stack =
new();
int number;
System.Collections.Generic.Stack<int>.Enumerator
enumerator;
// ...
// If IEnumerable<T> is implemented explicitly,
// then a cast is ((IIEnumerable<int>)stack).GetEnumerator();
enumerator = stack.GetEnumerator();
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
```

# ADVANCED/BEGINNER TOPIC

# Cleaning Up Following Iteration

Given that the classes that implement the IEnumerator<T> interface maintain the state, sometimes you need to clean up the state after it exits the loop (because either all iterations have completed or an exception is thrown). To achieve this, the IEnumerator<T> interface derives from IDisposable. Enumerators that implement IEnumerator do not necessarily implement IDisposable, but if they do, Dispose() will be called as well. This means that Dispose() can be called after the foreach loop. The C# equivalent of the final Common Intermediate Language (CIL) code, therefore, looks like Listing 15.7.

LISTING 15.7: Compiled Result of foreach on Collections

```
System.Collections.Generic.Stack<int> stack = new();
System.Collections.Generic.Stack<int>.Enumerator enumerator;
IDisposable disposable;
```

```
enumerator = stack.GetEnumerator();
try
{}
```