```
try
{
    Result = new Right<Exception, T>(@try());
}
catch (Exception e)
{
    Result = new Left<Exception, T>(e);
}
}
```

```
public void MatchWith((Action<T> Right, Action<Exception> Left) pattern) =>
    Result.MatchWith(pattern);
```

```
public Try<T1> Map<T1>(Func<T, T1> f) => new Try<T1>(() =>
Result.MatchWith<T1>(pattern: (
    Right: x => f(x),
    Left: e => throw e))
);
```

We could also postpone execution until instead trying to run the Func<T> @try immediately Right<Exception, T>(@try()).

Now that we have our Try in place, we can modify some of the functors that represent delayed computations like the Lazy, IO and Reader to Execute the contained computation in a safe manner that would yield an Either:

```
public static Try<T> ToTry<T>(this Lazy<T> @this) => new Try<T>(() => @this.Value);
```

Run This: .Net Fiddle

Language-Ext
Try<T>

There is an explicit implementation of Try<T> in the library you can find here