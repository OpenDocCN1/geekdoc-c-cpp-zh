If we use this on the head of the sub-list in each step we get the default Map:

**Map** ([ ], f) = [ ]

**Map** ([v , rest], f) = [f(v), **Map** (rest, f) ]

# 3.10 Returning More items

In a similar manner we can modify the **Rebuild** function to return a tuple (v, v * v) pairing the value with its square

```
List<(int, int)> Squares(List<int> @list) =>
    @list.MatchWith((
        Empty: () => new List<(int, int)> { },
        Cons: (v, rest) => ((v, v * v), Squares(rest)).AsList()
    ));
```

Symbolically:

**Squares** ([ ]) = [ ]

**Squares** ([v , rest]) = [(v, v²), **Squares** (rest) ]

Of course, we can do the same using only the **Map** function:

```
List<(int, int)> Squares(List<int> @list) => Map(@list, v => (v, v * v));
```

Or directly using Select:

```
List<(int, int)> Squares(List<int> @list)=> @list.Select(v =>(v, v*v)).ToList();
```

# 3.11 Filtering

Here we will add another Func<T, bool> @predicate parameter to the recursive Function, we are gong to use this @predicate to filter the Array using recursion. Symbolically, the **Filter** function:

**Filter** ([ ], predicate) = [ ]

**Filter** ([v , rest], predicate) = if( predicate (v) )
    [v , **Filter** (rest , predicate) ]
else
    **Filter** (rest , predicate)