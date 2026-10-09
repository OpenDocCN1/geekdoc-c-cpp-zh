That is why we use the `lock` statement everywhere we access the variable in `Playlist`. The variables of the collection type `IList<T>` are not "thread-safe", as we say, and they need to be "protected".

We also declare the `rng` variable of a type `Random` readonly.

```
private static readonly Random rng = new();
```

The `Random` type appears to be pretty much immutable. Once you set the seed, via the constructor, there is no way to "write" to the variable of type `Random`. (The default constructor of `Random` uses the current time as a seed by default.) But, again `Random` is not an immutable type by its very nature. First of all, it is a reference type. And, it is not a "data" type.

`Random` prescribes a behavior. It generates a sequence of random numbers. Depending on how you access it, you get a different number. They are "deterministic" (in the sense that they are "pseudo-random" numbers). Granted. Even so, suppose that you have the multiple threads that request the random numbers from the same `object`. They all may end up getting different sequences of numbers unless they are synchronized in some way. (As one can easily guess, `System.Random` is implemented as a class.)

As stated, the `readonly` keyword provides limited protections for the reference type variables. But, it is still recommended to use `readonly`, when applicable, at least to protect the references themselves, if not the data they are referencing.

The `Shuffle()` method returns a copy of itself, with its internal `Song` list shuffled. This is to preserve the original ordering, as indicated earlier.

Note that the `Shuffle()` method itself does not use the `lock` statement. The `Copy()` method is synchronized. In this particular case, that should be enough. You can also use nested `lock` statements, in which a `lock` statement block includes another `lock` statements (either directly or via another method call). Only the thread that currently has the outer `lock` can acquire any inner `lock`.