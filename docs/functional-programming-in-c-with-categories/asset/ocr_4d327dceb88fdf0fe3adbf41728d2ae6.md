```
ValueTuple<int> t1 = ValueTuple.Create(5);
```

Which has as its inverse the generic Fold implementation by Microsoft for Tuples:

```
static S Fold<A, S>(this System.ValueTuple<A> self, S state, System.Func<S, A, S> fold);
```

this is the standard Fold signature which is the equivalent of the List.Aggregate and we can use it to get the value back like this:

```
var value = t1.Fold(0, (a, e) => a + e);
```

![](bbox=[0.35, 0.275, 0.75, 0.34])

Finally, obviously ValueTuple<T> isomorphic to List<T> so we can create some extension methods to go from one to the other

```
static List<T> ToList<T>(this ValueTuple<T, T> @this) => new List<T> {
    @this.Item1,
    @this.Item2
};
```

ValueTuple is a Functor since is equivalent with the List () but just for fun we can create a ValueTuple .Map extension method directly :

```
static ValueTuple<T1, T1> Map<T, T1>(this ValueTuple<T,T> @this, Func<T, T1> f) => (f(@this.Item1), f(@this.Item2));
```

# SideNote:

A very obvious observation is that if we implemented ValueTuple<T, T>.ToList<T>() and ValueTuple<T1, T1>.Map<T, T1>(f) correctly then the results of the following expressions should be equal:

```
(3, 4).ToList().Select(x => x + 4);
(3, 4).Map(x => x + 4).ToList();
```

those two expressions represent the different paths in the following diagram:

![](bbox=[0.31, 0.77, 0.72, 0.88])