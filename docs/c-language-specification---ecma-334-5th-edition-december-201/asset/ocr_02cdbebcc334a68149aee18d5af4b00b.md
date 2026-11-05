```
class Extend : Base<int>    // Valid, non-constructed class with
// constructed base class
class Extend<V>: V {}        // Error, type parameter used as base class
class Extend<V> : Base<V> {} // Valid, type parameter used as type
// argument for base class
```

end example]

The direct base class of a class type shall be at least as accessible as the class type itself (§8.5.5). For example, it is a compile-time error for a public class to derive from a private or internal class.

The direct base class of a class type shall not be any of the following types: System.Array, System.Delegate, System.Enum, or System.ValueType. Furthermore, a generic class declaration shall not use System.Attribute as a direct or indirect base class (§22.2.1).

In determining the meaning of the direct base class specification A of a class B, the direct base class of B is temporarily assumed to be object, which ensures that the meaning of a base class specification cannot recursively depend on itself. [Example: The following

```
class X<T> {
    public class Y{}
}
class Z : X<Z.Y> {}
```

Is in error since in the base class specification X<Z.Y> the direct base class of Z is considered to be object, and hence (by the rules of §8.8) Z is not considered to have a member Y. end example]

The base classes of a class are the direct base class and its base classes. In other words, the set of base classes is the transitive closure of the direct base class relationship. [Example: In the following:

```
class A {...}
class B<T>: A {...}
class C<T>: B<IComparable<T>> {...}
class D<T>: C<T[]> {...}
```

the base classes of D<int> are C<int[]>, B<IComparable<int[]>>, A, and object.
end example]

Except for class object, every class has exactly one direct base class. The object class has no direct base class and is the ultimate base class of all other classes.

It is a compile-time error for a class to depend on itself. For the purpose of this rule, a class directly depends on its direct base class (if any) and directly depends on the nearest enclosing class within which it is nested (if any). Given this definition, the complete set of classes upon which a class depends is the transitive closure of the directly depends on relationship.

[Example: The example

```
class A: A {}
```

Is erroneous because the class depends on itself. Likewise, the example

```
class A: B {}
class B: C {}
class C: A {}
```

is in error because the classes circularly depend on themselves. Finally, the example

```
class A: B.C {}
```