A generic type can implement a generic interface. The same is possible by deriving from a class. A generic class can be derived from a generic base class:

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<T>
{
}
```

The requirement is that the generic types of the interface must be repeated, or the type of the base class must be specified, as in this case:

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<string>
{
}
```

This way, the derived class can be a generic or non-generic class. For example, you can define an abstract generic base class that is implemented with a concrete type in the derived class. This enables you to write *generic specialization* for specific types:

```
public abstract class Calc<T>
{
    public abstract T Add(T x, T y);
    public abstract T Sub(T x, T y);
}
```

```
public class IntCalc: Calc<int>
{
    public override int Add(int x, int y) => x + y;
    public override int Sub(int x, int y) => x - y;
}
```

You can also create a partial specialization, such as deriving the `StringQuery` class from `Query` and defining only one of the generic parameters, for example, a `string` for `TResult`. For instantiating the `StringQuery`, you need only to supply the type for `TRequest`:

```
public class Query<TRequest, TResult>
{
}
```

```
public StringQuery<TRequest> : Query<TRequest, string>
{
}
```

# Static Members

Static members of generic classes are shared with only one instantiation of the class, and they require special attention. Consider the following example, where the class `StaticDemo<T>` contains the