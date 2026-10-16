```
public T Value { get; set; }
public Id(T value) => Value = value;

public T1 MatchWith<T1>(Func<T, T1> callback) => callback(Value);
public void MatchWith(Action<T> callback) => callback(Value);
}
```

![](bbox=[0.58, 0.19, 0.79, 0.24])

```
new Id<int>(3).MatchWith(Console.WriteLine);
```

```
Console.WriteLine( new Id<int>(3).value)    // Instead of this
```

If we want to get just the value we can pass the identity function inside

```
var value =new Id<int>(3).MatchWith (x=>x);
```

here we are going to use the for the first time the C#8.0 pattern matching in a trivial way.
Take a look :

```
string result = new Id<int>(5)
    switch
    {
        Id<int> { Value: var v } => v.ToString(),
    };
```

Using the following switch syntax:

```
switch
{
    _ =>
};
```

We can peak inside the Id<int>( )

```
switch
{
    Id<int> { } => _
};
```

and match the value (access the value, make a claim about how the Id<int>( ) looks if dissected)

```
switch
{
    Id<int> { Value: var v } => _
};
```