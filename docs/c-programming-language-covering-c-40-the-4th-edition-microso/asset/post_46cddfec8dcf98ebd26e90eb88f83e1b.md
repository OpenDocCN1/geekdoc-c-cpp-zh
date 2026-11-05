
> **CHRIS SELLS** For readability, foreach statements should be preferred over for statements.

> **JON SKEET** The fact that there is *one* iteration variable (which is read-only and yet magically changes its value on each iteration) causes one of the most common problems with captured variables. The code below looks like it would print “a”, “b”, “c”, “d” but it actually prints “d” four times.

```csharp
List<Action> actions = new List<Action>();
foreach (string value in new[] { "a", "b", "c", "d" })
{
    actions.Add(() => Console.WriteLine(value));
}
foreach (Action action in actions)
{
    action();
}
```

> The solution is usually to introduce an extra variable inside the body of the foreach statement that takes a copy of the iteration variable's current value. That way each delegate will capture a different variable. In this case, the first loop would become

```csharp
foreach (string value in new[] { "a", "b", "c", "d" })
{
    string copy = value;
    actions.Add(() => Console.WriteLine(copy));
}
```

> **PETER SESTOFT** The foreach statement might have been defined differently to avoid the variable capture problem discussed in Jon Skeet's comment: Simply move the declaration `v` inside the while loop in the try-while-finally expansion shown later in this section. Indeed, in the original C# language specification, the declaration appeared inside the while loop, but during standardization of C# 2.0 it turned out that declaring `v` outside the loop was closer to the truth, at least in Microsoft's implementation, and the standard was changed accordingly.

The compile-time processing of a foreach statement first determines the *collection type*, *enumerator type*, and *element type* of the expression. This determination proceeds as follows:

- If the type X of *expression* is an array type, then there is an implicit reference conversion from X to the `System.Collections.IEnumerable` interface (since `System.Array` implements this interface). The *collection type* is the `System.Collections.IEnumerable` interface, the *enumerator type* is the `System.Collections.IEnumerator` interface, and the *element type* is the element type of the array type X.
- If the type X of *expression* is *dynamic*, then there is an implicit conversion from *expression* to the `System.Collections.IEnumerable` interface (§6.1.8). The *collection type* is the `System.Collections.IEnumerable` interface and the *enumerator type* is the `System.Collections.IEnumerator` interface. If the *var* identifier is given as the *local-variable-type*, then the *element type* is *dynamic*; otherwise, it is *object*.
- Otherwise, determine whether the type X has an appropriate GetEnumerator method:
  - Perform member lookup on the type X with identifier GetEnumerator and no type arguments. If the member lookup does not produce a match, or if it produces an ambiguity or a match that is not a method group, check for an enumerable interface as described below. It is recommended that a warning be issued if member lookup produces anything except a method group or no match.

> > **ERIC LIPPERT** This “pattern”-based approach was specified so that back in the days before the generic `IEnumerable<T>` was available, collection authors could provide stronger type annotations on their enumerator objects.
> >
> > Implementations of nongeneric `IEnumerable` always end up boxing every member of a collection of integers because the return type of the Current property is object. A provider of a collection of integers could provide non-interface-based GetEnumerator, MoveNext, and Current implementations such that Current returns an unboxed integer.
> >
> > Of course, in a world with generic `IEnumerable<T>`, all of this effort becomes unnecessary. The vast majority of iterated collections will implement this interface.

- Perform overload resolution using the resulting method group and an empty argument list. If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, check for an enumerable interface as described below. It is recommended that a warning be issued if overload resolution produces anything except an unambiguous public instance method or no applicable methods.
- If the return type E of the GetEnumerator method is not a class, struct, or interface type, an error is produced and no further steps are taken.

- Member lookup is performed on E with the identifier Current and no type arguments. If the member lookup produces no match, the result is an error, or the result is anything except a public instance property that permits reading, an error is produced and no further steps are taken.
- Member lookup is performed on E with the identifier MoveNext and no type arguments. If the member lookup produces no match, the result is an error, or the result is anything except a method group, an error is produced and no further steps are taken.
- Overload resolution is performed on the method group with an empty argument list. If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, or its return type is not bool, an error is produced and no further steps are taken.
- The collection type is X, the enumerator type is E, and the element type is the type of the Current property.
- Otherwise, check for an enumerable interface:
  - If there is exactly one type T such that there is an implicit conversion from X to the interface System.Collections.Generic.IEnumerable<T>, then the collection type is this interface, the enumerator type is the interface System.Collections.Generic.IEnumerator<T>, and the element type is T.
  - Otherwise, if there is more than one such type T, then an error is produced and no further steps are taken.
  - Otherwise, if there is an implicit conversion from X to the System.Collections.IEnumerable interface, then the collection type is this interface, the enumerator type is the interface System.Collections.IEnumerator, and the element type is object.
  - Otherwise, an error is produced and no further steps are taken.

> > **PETER SESTOFT** Sadly, the compile-time processing of the foreach statement means that it is rather dynamically typed. For instance, for an arbitrary non-sealed class C and interface I, the following is type correct and causes no compiler warnings or errors:

```csharp
C[] xs = ...;
foreach (I x in xs)
...
```

> > In fact, just recently I fell into this trap when removing a seemingly irrelevant interface I from the interface list of a class C. The project went through the build stage without errors, but at runtime the application crashed with an InvalidCastException because I had overlooked several foreach statements. Actually, this behavior should be expected, because there might be some subclass of C that implements interface I. What is perhaps more surprising is that I and C can be swapped in the preceding code with the same result.

The above steps, if successful, unambiguously produce a collection type C, enumerator type E, and element type T. A foreach statement of the form

`foreach (V v in x) embedded-statement`

is then expanded to:

```csharp
{
    E e = ((C)(x)).GetEnumerator();
    try {
        V v;
        while (e.MoveNext()) {
            v = (V)(T)e.Current;
            embedded-statement
        }
    }
    finally {
        ... // Dispose of e
    }
}
```

The variable e is not visible to or accessible to the expression x, the embedded statement, or any other source code of the program. The variable v is read-only in the embedded statement. If there is not an explicit conversion (§6.2) from T (the element type) to V (the local-variable-type in the foreach statement), an error is produced and no further steps are taken. If x has the value null, a System.NullReferenceException is thrown at runtime.

> > **MAREK SAFAR** The foreach statement is a classic example of language evolution. C# 1.0 did not have the generic IEnumerable<T> and explicit conversion had to be used from element type to local variable. C# 2.0 introduced a generic version of the foreach statement with an element of a generic type. C# 3.0 brought this structure back to where it should have been at the beginning by introducing *implicitly typed iteration variable*, which changes explicit conversion to be implicit and avoids any InvalidCastException during execution.
