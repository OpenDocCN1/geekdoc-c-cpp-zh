```
{
  static void Main()
  {
    var rabbits = new[] { 1, 1, 2, 3, 5, 8, 13, 21, 34, 55 };
    var evenRes = rabbits.Where(x => x % 2 == 0);
    ...
  }
}
```

Again, the use of using directives is a compile-time thing only because the above is turned into a static Where method call, defined on the System.Linq.Enumerable static class, which lives in the System.Core assembly:

```
var evenRes = Enumerable.Where(rabbits, x => x % 2 == 0);
```

The Where method becomes available for resolution once the System.Linq namespace gets imported. Figure 24.16 illustrates that Visual Studio has special knowledge about the usage pattern of extension methods when using query comprehension syntax.

![](bbox=[0.08, 0.62, 0.55, 0.78])

FIGURE 24.16 Visual Studio knows about the LINQ extension methods.

In System.Core, the Where method is defined as follows, highlighting the essential bits that comprise an extension method definition:

```
// Somewhere in System.Core
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
            Func<T, bool> predicate) { ... }
    }
}
```

Extension methods are resolved by searching for them in enclosing as well as imported namespaces. Instance methods take precedence if an applicable overload is available,