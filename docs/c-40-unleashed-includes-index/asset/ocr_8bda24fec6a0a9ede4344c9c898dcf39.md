![](bbox=[0.069, 0.079, 0.563, 0.271])

FIGURE 16.7  Stronger type checking enforced by generics.

Notice how the example uses an implicitly typed local variable for the foreach loop’s iteration variable. Because all type information around generics is known at compile time, as proven by the great IntelliSense experience, the compiler can infer statically what the loop variable’s type ought to be. This is proven by code editor inspection in Figure 16.8.

![](bbox=[0.072, 0.451, 0.518, 0.572])

FIGURE 16.8  Rich type information available at compile time.

While we’re at it, direct iteration over dictionary types (as opposed to going over keys or values individually) is also possible. By looking at the definition of the generic type, you can trace why this is the case:

```
```csharp
public class Dictionary<TKey, TValue> : IDictionary<TKey, TValue>, ...
```
```

From here, we get into the IDictionary<TKey, TValue> generic interface, which in turn leads us to an ICollection generic interface:

```
```csharp
public interface IDictionary<TKey, TValue> :
    ICollection<KeyValuePair<TKey, TValue>>
```
```

Here things start to get more interesting: The ICollection<T> interface is parameterized with the KeyValuePair<TKey, TValue> generic type. But first, let’s finish our tracing of the enumerable nature of a generic dictionary by following the ICollection<T> trail:

```
```csharp
public interface ICollection<T> : IEnumerable<T>
```
```