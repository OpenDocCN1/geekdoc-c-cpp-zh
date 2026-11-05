You must assign a value when using var, otherwise the compiler has nothing to infer the type from. For example, var x; is invalid — but var x = 5; is fine.

This makes code cleaner, especially when dealing with complex types:

```
var orders = new Dictionary<string, List<int>>();
```

...instead of:

```
Dictionary<string, List<int>> orders = new Dictionary<string, List<int>>();
```

But use var wisely: overusing it can make code harder to read if the type is not obvious from context.

# [Supplement]

The use of var does not mean dynamic typing — it's still strongly typed.

Avoid using var when it makes the code unclear.

Useful with LINQ or anonymous types, where the exact type is long or unknown.