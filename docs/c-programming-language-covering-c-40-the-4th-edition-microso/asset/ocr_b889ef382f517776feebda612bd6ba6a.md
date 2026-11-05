# 10.3.2 Members of Constructed Types

The non-inherited members of a constructed type are obtained by substituting, for each *type-parameter* in the member declaration, the corresponding *type-argument* of the constructed type. The substitution process is based on the semantic meaning of type declarations, and is not simply textual substitution.

For example, given the generic class declaration

```
~~~
class Gen<T,U>
{
    public T[,] a;

    public void G(int i, T t, Gen<U,T> gt) {...}

    public U Prop { get {...} set {...} }

    public int H(double d) {...}
}
~~~
```

the constructed type Gen<int[,],IComparable<string>> has the following members:

```
~~~
public int[,][] a;

public void G(int i, int[,] t, Gen<IComparable<string>,int[,]> gt) {...}

public IComparable<string> Prop { get {...} set {...} }

public int H(double d) {...}
~~~
```

The type of the member *a* in the generic class declaration *Gen* is “two-dimensional array of *T*,” so the type of the member *a* in the constructed type above is “two-dimensional array of one-dimensional array of int,” or int[,][].

Within instance function members, the type of *this* is the instance type (§10.3.1) of the containing declaration.

> **JON SKEET**  This treatment of generics via substitution leads to obvious tricky situations. What would the following code do?

```
~~~
public class Puzzle<T> {
    public void Method(int i) {}
    public void Method(T t) {}
}
...
new Puzzle<int>().Method(10);
~~~
```

> The “substitution” results in two methods with exactly the same signature—so which one is called by the Method(10) expression? I readily admit that I wouldn't know the answer without looking it up or trying it. I strongly suggest that such ambiguity should be avoided wherever possible. In my experience, it's most likely to occur with a pair of indexers that can look an item up either by position (an int) or key (a type parameter).