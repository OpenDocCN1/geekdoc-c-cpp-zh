# Chapter 13: Delegates and Lambda Expressions

```
public delegate TResult Func<out TResult>();
public delegate TResult Func<in T, out TResult>(T arg);
public delegate TResult Func<in T1, in T2, out TResult>(
T1 arg, T2 arg);
public delegate TResult Func<in T1, in T2, in T3, out TResult>(
T1 arg, T2 arg, T3 arg);
public delegate TResult Func<in T1, in T2, in T3, in T4,
out TResult>(T1 arg, T2 arg, T3 arg, T4 arg);
...
```

```
public delegate TResult Func<
in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8,
in T9, in T10, in T11, in T12, in T13, in T14, in T15, in T16,
out TResult>(
T1 arg, T2 arg, T3 arg, T4 arg;
T5 arg, T6 arg, T7 arg, T8 arg;
T9 arg, T10 arg, T11 arg, T12 arg;
T13 arg, T14 arg, T15 arg, T16 arg);
```

```
public delegate bool Predicate<T>(T obj)
```

Since the delegate definitions listed in Listing 13.4 are generic, you can use instead of defining your own delegate.

The first delegate type in Listing 13.4 is Action<...>. It is used to represent a method for which there is no return result, and supports methods up to 16 parameters. For delegates that need to return a result, there is the Func<...> delegate. The last type parameter of Func<...> is TResult—the type of the return. The other type parameters on Func<...> correspond in sequence to the types of the delegate parameters. The BubbleSort method in Listing 13.3, for example, requires a delegate that returns bool and takes two parameters.

The last delegate in Listing 13.4 is Predicate<T>. When a lambda is used to return a bool, the lambda is called a predicate. However, this predicate is generally used to filter or identify items from a collection—you pass an item and it returns true or false to indicate whether or not to filter the item. In contrast, the BubbleSort() example accepted two parameters for the purpose of comparing them, so Func<int, int, bool> was used instead of a predicate type.