```
var listOfTrees = new List<Tree<int>>() {
    new Node<int>(new Leaf<int>(2), new Node<int>(new Leaf<int>(2), new Leaf<int>(4)))
    , new Node<int>(new Leaf<int>(2), new Leaf<int>(4)) };

var traversedList = listOfTrees.TraverseT(x => new Id<int>(x + 1));
```

You can try other variations like composing trees etc. by forking some of the previous Fiddles. I think that traversable is an underrated concept and there should be used more often in real situations.

# 7.5 Foldable

Within the same paper of "Applicative Programming with Effects" Conor McBride and Ross Paterson used an applicative constant functor based on a monoid, in order to use it with a traversable, to perform the accumulation. I was planning to present this way of connecting Traversables with Foldables here but because of C# typing I think it only would make things much more difficult to follow.

Instead, we will go straight to some implementations of Fold on lists and Trees. Let’s start by defining Fold on a List (this is basically the Enumerable.Aggregate. Unfortunately, the .NET framework designers faced with a dilemma when naming the Aggregate function on the one hand they had to follow the whole LINQ idea and comply to the SQL naming, and on the other side was the default functional naming of Fold. They chose the SQL naming convention)

```
public static T Fold<T>(this List<T> @this, (Func<T> empty, Func<T, T, T> concat) monoid)
    =>
    @this.MatchWith(algebra: (
        Empty: monoid.empty,
        Cons: (v, r) => monoid.concat(v, r.Fold(monoid))
    ));
```

Run This: .Net Fiddle

Here we have a List and a monoid (Func<T> empty, Func<T, T, T> concat) in its simple Tuple form and we end up with a single type T in the next section of FoldMap we will see the more generic case where the T does not have to be a monoid but we have to provide a function Func<T, TM> f that converts it into a monoid TM

The Type definition of Fold is this:

```
Fold: t(a) → m    // where t : traversable and m: monoid
```

Now let’s define the same thing for a Tree: