![](bbox=[0.26, 0.13, 0.73, 0.31])

As you can see, those two implementations are pretty much equivalent. We can argue which one is better, but the object-oriented implementation looks easier. Easy, intuitive implementation is one of the advantages of object-oriented programming, even if the interpreter design pattern is not used often in development. On the opposite side, functional applicative implementation in my opinion looks prettier.

# 7.4 Explicitly Composing Traversables

Traversables are closed under composition. We can formulate a valid traverse operation for our two functor composition by just pushing the traverse operation to the inner functor and then traverse with this function the inner Functor. Unfortunately, there are no Higher Kind Types in C# so you have to rewrite the above implementation using the specific Traversables that you want to compose.

```
public static Id<List<Tree<T>>> TraverseT<T>(this List<Tree<T>> @this, Func<T, Id<T>> f) => @this.Traverse(x => x.Traverse(f));
```

```
public static Id<Tree<List<T>>> TraverseT<T>(this Tree<List<T>> @this, Func<T, Id<T>> f) => @this.Traverse(x => x.Traverse(f));
```

The first can traverse this Tree of Lists<int>

```
var treeOfLists = new Node<List<int>>(new Leaf<List<int>>(new List<int>() { 1, 2 })
, new Node<List<int>>(new Leaf<List<int>>(new List<int>() { 3, 4 }),
new Leaf<List<int>>(new List<int>() { 5, 6 })));
```

```
var traversedTree = treeOfLists.TraverseT(x => new Id<int>(x + 1));
```

and the second can traverse this