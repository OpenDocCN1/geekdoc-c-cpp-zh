```
public static T Fold<T>(this Tree<T> @this, (Func<T> empty, Func<T, T, T> concat) monoid)
    =>
    @this.MatchWith(pattern: (
    Leaf: v => monoid.concat(monoid.empty(), v),
    Node: (l, r) => monoid.concat(l.Fold(monoid), r.Fold(monoid))
    ));
```

```
var tree = new Node<int>(new Leaf<int>(2), new Node<int>(new Leaf<int>(2), new Leaf<int>(4)));
var r = tree.Fold(monoid: (() => 0, (x, y) => x + y));
```

alternatively we can use the Array as a monoid and thus convert a tree into a map by folding with the list monoid ([,])

```
var tolist = tree.Map(x => x.AsList())
.Fold(monoid: (() => new List<int>(), (x, y) => x.Concat(y)));
```

but we had to map to a list first Map(x => x.AsList()) in order to use this definition of Fold. We could define a new Method to do this Mapping together with the Fold. This is called traditionally FoldMap and is the topic of the next section.

# 7.5.1 FoldMap

Let’s discuss foldMap a bit more. FoldMap takes a function that return a monoid (a→m) and apply it on a traversable in order to get a single value of type m. This is actually a variation of Fold.

Foldmap: (a→m) → t(a) → m where m is a monoid

So, we define FoldMap directly from fold like below

```
public static TM FoldMap<T, TM>(this Tree<T> @this,
    (Func<TM> empty, Func<TM, TM, TM> concat) monoid, Func<T, TM> f)
    =>
    @this.MatchWith(pattern: (
        Leaf: v => monoid.concat(monoid.empty(), f(v)),
        Node: (l, r) => monoid.concat(l.FoldMap(monoid, f), r.FoldMap(monoid, f))
    ));
```

In some cases, we can just omit the demand for both

![](bbox=[0.68, 0.27, 0.88, 0.32])