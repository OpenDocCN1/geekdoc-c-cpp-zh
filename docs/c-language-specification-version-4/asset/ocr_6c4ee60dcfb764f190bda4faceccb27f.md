```
I<int> x = new X<int,int>();
x.F();
```

To determine if the interface list of a generic type declaration is valid, the following steps are performed:

+   - Let L be the list of interfaces directly specified in a generic class, struct, or interface declaration C.
+   - Add to L any base interfaces of the interfaces already in L.
+   - Remove any duplicates from L.
+   - If any possible constructed type created from C would, after type arguments are substituted into L, cause two interfaces in L to be identical, then the declaration of C is invalid. Constraint declarations are not considered when determining all possible constructed types.

In the class declaration X above, the interface list L consists of I<U> and I<V>. The declaration is invalid because any constructed type with U and V being the same type would cause these two interfaces to be identical types.

It is possible for interfaces specified at different inheritance levels to unify:

```
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {}
}
class Derived<U,V>: Base<U>, I<V>  // Ok
{
    void I<V>.F() {...}
}
```

This code is valid even though Derived<U,V> implements both I<U> and I<V>. The code

```
I<int> x = new Derived<int,int>();
x.F();
```

invokes the method in Derived, since Derived<int,int> effectively re-implements I<int> (§13.4.6).

# 13.4.3 Implementation of generic methods

When a generic method implicitly implements an interface method, the constraints given for each method type parameter must be equivalent in both declarations (after any interface type parameters are replaced with the appropriate type arguments), where method type parameters are identified by ordinal positions, left to right.

When a generic method explicitly implements an interface method, however, no constraints are allowed on the implementing method. Instead, the constraints are inherited from the interface method

```
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}
class C: I<object,C,string>
{
    public void F<T>(T t) {...}            // Ok
    public void G<T>(T t) where T: C {...} // Ok
    public void H<T>(T t) where T: string {...} // Error
}
```