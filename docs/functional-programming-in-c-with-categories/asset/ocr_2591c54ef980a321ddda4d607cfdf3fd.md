It is passing a lambda inside the constructor of our data structure

```
⟨_ _ _⟩
(x=>y=>_ concat _)
Id(x => y => x.concat(y)).app(_).app(_ );
```

Here we have placed the curried concat function (_=>_=>_.concat_) Inside an applicative in order to be able to chain the applicative calls. In Haskell, for example, this is called sequenceA :: Applicative f => t (f a) → f (t a), and what does is to take a traversable t that contains f(a) items and evaluates them and collect the results.

Why get into all this trouble just to get an Id ([1, 2, 3]) ? Well, we can abstract the Id and have a function a → Id(b) that will do the generation of the Id ([_]). We get this implementation:

```
public static Id<List<T1>> Traverse<T,T1>(this List<T> @this,Func<T, Id<T1>> f)
=>
    @this.MatchWith(pattern: (
        Empty: ()      => new Id<List<T1>>(new List<T1>()),
        Cons : (v, r) =>
        new Id<Func<T1, Func<List<T1>, List<T1>>>>(x =>y =>x.AsList().Concat(y))
        .Ap(f(v))
        .Ap(r.Traverse(f))
    ));
var result = [2, 3, 5].Traverse( IdF, v => IdF(v + 1));
```

Here the f is the applicative functor constructor, aka pure (_) in the fiddle is written as TyperRep for Type Representable, (TypeRep is the constructor of the Functor). In a symbolic notation, it could be described as follows:

```
traverse: Applicative f : (a → f(b)) → [ a ] → f [ b ]

traverse (f, []) = ⟨ [] ⟩

traverse (f, [value, rest]) = ⟨ (.) f(value) (traverse( f, rest)) ⟩
```

now if you compare the signatures of the distribute and traverse you can see that we can create traverse from distribute by first mapping the (a → f(b)) on the array elements so we get:

[ a ].map(a → f(b)) → [f(b)] and then apply the distribute to get the final f [ b ] So :

list .traverse (g) = list .map(g). distribute ( ) where g : a → f(b) :

```
var TraverseEquivalent= (list,g)=>list.map(g).distribute();
```