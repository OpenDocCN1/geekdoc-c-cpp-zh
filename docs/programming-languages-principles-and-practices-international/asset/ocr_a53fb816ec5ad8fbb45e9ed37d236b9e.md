# Figure 8.18 Further substitutions

(δ = α because the result type of the if expression is now α, and this is the type of the body of the function; hence the return type of the body.) Thus, max has been determined to have type α (*) (α, α, bool (*) (α, α)), where α is any type—in other words, a type parameter that can have any actual type substituted for it. In ML this type is printed as:

```
`a * `a * (`a * `a -> bool) -> `a
```

where `a is used instead of the type variable α, a function type is indicated by the arrow ->, and the multiple parameters are represented by a tuple (or Cartesian product) type²² (the Cartesian product A × B in ML is printed as A*B and values of this type are written as tuples (a, b) with α ∈ A and b ∈ B).

With this typing for the function max, we can use max in any situation where the actual types unify with the polymorphic type. For example, if we provide the following definitions in ML:

```
fun gti (x:int,y) = x > y;
fun gtr (x:real,y) = x > y;
fun gtp ((x,y),(z,w)) = gti (x,z);
```

we can call the max function as follows:

```
max(3,2,gti); (* returns 3 *)
max(2.1,3.2,gtr); (* returns 3.2 *)
max((2,"hello"),(1,"hi"),gtp); (* returns (2,"hello") *)
```

Note that α (*) (α, α, bool (*) (α, α)) really is the most general type possible for the max function with the given implementation (called its principal type), and that each call to max specializes this principle type to a monomorphic type, which may also implicitly specialize the types of the parameters. For example, the type of the gtp function is bool (*) ((int,α),(int,β)) (or (int * `a) * (int * `b) -> bool in ML syntax), with two type variables for the types of y and w, since these two variables are not used in the body of gtp, so each can be of any type. Now, in the call to max above, we still could not use two different types for y and w, since the max function insists on the same type for the first two parameters:

²In fact, we have written the parameters (x, y, gt) in tuple notation in the definition. It is possible to write them differently, resulting in what is called a Curried function. This was discussed in Chapter 4.