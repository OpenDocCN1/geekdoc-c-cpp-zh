```
.Ap(new Id<List<int>>((3, 6).ToList()));
// Id([10,5,3,6])
```

we can do that repeatedly by replacing the last Ap() with the whole structure since it is of the same type:

```
new Id<Func<List<int>, Func<List<int>, List<int>>>>(x => y => x.Concat(y))
    .Ap(new Id<List<int>>((10, 5).ToList()))
    .Ap(new Id<Func<List<int>,Func<List<int>,List<int>>>>(x =>y=>x.Concat(y))
        .Ap(new Id<List<int>>((10, 5).ToList()))
        .Ap(new Id<List<int>>((3, 6).ToList()))
    );
```

we can use recursion to use this in any list:

```
public static Id<List<T>> Distribute<T>(this List<Id<T>> @this,
    Func<Id<List<T>>> TypeRep) =>
    @this.MatchWith(algebra: (
        Empty: ()      => TypeRep(),
        Cons : (v, r) =>
    new Id<Func<List<T>, Func<List<T>, List<T>>>>(x =>y=>x.Concat(y))
        .Ap(v.Map(x => x.ToList()))
        .Ap(r.Distribute(TypeRep))
    ));
```

```
new List<Id<int>> { new Id<int>(2), new Id<int>(3) }
    .Distribute<int>(() => new Id<List<int>>(new List<int>())); //Id([2, 3])
```

Inside the paper that introduced the concept of applicatives "Applicative Programming with Effects" Conor McBride and Ross Paterson called this applicative distributor for lists:

```
distribute:: Applicative f : [f a ] ⟶ f [ a ]      // the f from inside the list goes to the outside
distribute ([]) = ⟨ [] ⟩
distribute ([value: rest]) = ⟨ (:) value (distribute (rest)) ⟩
```

compare this to the map

```
map f ([ ]) = [ ]
map f ([value: rest]) = [ f(value): map f (rest)]
```

this is a loose representation where the ⟨...⟩ represents the applicative operation.

the ⟨ (concat) __ ⟩ represents the following expression when our f is the Id applicative functor :

```
Id(x => y => x.concat(y)).app(_).app(_);
```