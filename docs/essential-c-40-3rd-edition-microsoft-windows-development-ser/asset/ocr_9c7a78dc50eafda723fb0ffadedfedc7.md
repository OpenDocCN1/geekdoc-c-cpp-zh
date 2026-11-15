of type Action<object>. In other words, any methods with a void return and an object parameter will implicitly cast to the more restrictive delegate type that only allows parameters of type string. Similarly with covariance and a Func delegate—since Result<T Func<out TResult>() includes the out type parameter modifier on TResult, it is possible to implicitly assign a Func<object> variable the value of a Func<string>. (See Listing 12.14.)

# LISTING 12.14: Using Variance for Delegates

```
// Covariance
Action<object> broadAction =
    delegate(object data)
    {
        Console.WriteLine(data);
    };

Action<string> narrowAction = broadAction;

// Contravariance
Func<string> narrowFunction =
    delegate()
    {
        return Console.ReadLine();
    };

Func<object> broadFunction = narrowFunction;

// Covariance & Contravariance Combined
Func<object, string> func1 =
    delegate(object data)
    {
        return data.ToString();
    };

Func<string, object> func2 = func1;
```

The last part of the listing combines both variance concepts into a single example, demonstrating how they can occur simultaneously if both in and out type parameters are involved.

The need for variance support within these generic delegates was a key contributing factor why C# now includes the feature.²

2. The other was support for covariance to IEnumerable<T>.