```
class Derived: Base
{
    public class Nested
    {
        public void G() {
            Derived d = new Derived();
            d.f();        // Okay
        }
    }
}
class Test
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

the nested class Derived.Nested accesses the protected method F defined in Derived’s base class, Base, by calling through an instance of Derived.

# 10.3.8.6 Nested Types in Generic Classes

A generic class declaration can contain nested type declarations. The type parameters of the enclosing class can be used within the nested types. A nested type declaration can contain additional type parameters that apply only to the nested type.

Every type declaration contained within a generic class declaration is implicitly a generic type declaration. When writing a reference to a type nested within a generic type, the containing constructed type, including its type arguments, must be named. However, from within the outer class, the nested type can be used without qualification; the instance type of the outer class can be implicitly used when constructing the nested type. The following example shows three different—and correct—ways to refer to a constructed type created from Inner; the first two are equivalent:

```
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }
    static void F(T t) {
        Outer<T>.Inner<String>.F(t, "abc");  // These two statements
        Inner<String>.F(t, "abc");           // have the same effect
        Outer<int>.Inner<string>.F(3, "abc"); // This type is different
        Outer.Inner<string>.F(t, "abc");      // Error: Outer needs type arg
    }
}
```