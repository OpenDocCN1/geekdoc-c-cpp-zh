# 4.5 Id<T> Functor on the Fly

We can use extension methods to allow the creation an Id<T> from a value T and use the Map immediately and then Fold.

```
public static Id<T> ToId<T>(this T @this) => new Id<T>(@this);
```

And thus write:

```
(5).ToId()
.Map(x => x + 1)
.MatchWith(Console.WriteLine);
```

Is this useful? maybe, maybe not. but it signifies a way of writing that is very common in Functional programming using chaining and using transformation methods like .ToId() In order to move from one data structure into another.

The Id<T> and the T are isomorphic. They contain the exact same information and thus we can go back and forth without losing any information or needing any additional information by using the methods ToId<T> and Fold() (which are inverses in a sense)

![](bbox=[0.33, 0.45, 0.65, 0.5])

throughout this book we will see many isomorphisms. Those isomorphisms in the case of Functors are called Natural Transformations. We will see them in more detail in a latter chapter. For now, we are going to see four more isomorphisms (Task, Func, Lazy, IO) with the plain value T and thus provide you with a unifying abstraction when dealing with them.

# 4.5.1 Some more Isomorphisms

But first lats create another functor related to T. The value just T can be seen as a List with only one element:

```
public static List<T> ToList<T>(this T @this) => new List<T> { @this };
```

its inverse is the First() since for example 5.ToList().First()==5;

![](bbox=[0.34, 0.79, 0.62, 0.84])

T also is a ValueTuple with one element