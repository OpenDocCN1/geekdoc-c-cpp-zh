```
~~~csharp
// GetEnumerator -- This is the iterator block, which carries
//     out the actual iteration for the iterator object.
public System.Collections.IEnumerator GetEnumerator()
{
    // Iterate the associated collection's underlying list,
    // which is accessible because it's declared internal.
    foreach (string s in _mc._list)
    {
        yield return s;    // The iterator block's heart
    }
}
~~~
```

The collection in `IteratorBlockIterator` isn't much to write home about: a simple class wrapped around a `List` of strings. Its `GetEnumerator()` method simply returns a new instantiation of the companion iterator class, as in `LinkedList`:

```
~~~csharp
// GetEnumerator -- As in LinkedList, returns one of your
//     iterator objects.
public MyCollectionIterator GetEnumerator()
{
    return new MyCollectionIterator(this);
}
~~~
```

It's what's inside that iterator class that's interesting. It too contains a `GetEnumerator()` method. Implemented with an iterator block, this one does the iteration work. Here's that method:

```
~~~csharp
// GetEnumerator -- This is the iterator block, which carries
//     out the actual iteration for the iterator object.
public System.Collections.IEnumerator GetEnumerator()
{
    // Iterate the associated collection's underlying list,
    // which is accessible because it's declared internal.
    foreach (string s in mc._list)
    {
        yield return s;    // The iterator block's heart
    }
}
~~~
```

This method has access to the companion collection's contained `List<string>`, so its `yield return` statement can return each string in turn.

But the payoff is in `Main()`, where two copies of the iterator object are created. The `foreach` loop for the second one is nested in the `foreach` loop for the first, so the output looks like this:

```
~~~
Joe
Bob
Tony

Fred    Bob is Tony's boss
~~~
```