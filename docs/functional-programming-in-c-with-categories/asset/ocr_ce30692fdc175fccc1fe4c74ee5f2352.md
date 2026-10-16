# 3.4.3 The C#8.0 Pattern matching Feature

> -"function follows form."

After C# 8.0 we have case-analysis capabilities on polymorphic types natively. We can now skip the custom implementation of the MatchWith and instead use the switch statement :

```
public static T Multiply<T>(this ListBase<T> @this,
    (Func<T, T, T> concat, T empty) monoid) =>
    @this switch
    {
        Empty<T> { } => monoid.empty,
        Cons<T> { Value: var value, Rest: var rest } =>
            monoid.concat(value, rest.Multiply(monoid))
    };
```

Run This: .Net Fiddle

We are going to discuss more C# 8.0 pattern matching in the Functors example. But immediately you can see that you don’t need to modify your types at all in order to add polymorphic functions. The only drawback is that you have to expose the properties that you want to access as public (alternatively you have to define type destructors that will decompose the type into the values)

# 3.5 A brief intro to Recursion

> "Did you mean: recursion"
> -Google Search

> "Hofstadter's Law: It always takes longer than you expect, even when you take into account Hofstadter's Law."
> - Hofstadter's Law

**Recursion** occurs when a thing is defined in terms of itself or of its type. The importance of recursion in human thought, computer science and functional programming in particular is immense. We will be using Recursion throughout the book. For this reason, I won’t go into an introductory explanation. Instead, we are going to have a light exploration of the Recursion in the C# type system. The easiest way to give a Recursive definition in C# would be :

```
public T F<T>() => F<T>();
```