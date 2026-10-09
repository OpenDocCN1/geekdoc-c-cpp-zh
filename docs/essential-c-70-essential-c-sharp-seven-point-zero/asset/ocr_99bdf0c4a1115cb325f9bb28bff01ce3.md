```
interface ICompareThings<in T>
{
    bool FirstIsBetter(T t1, T t2);
}
```

```
class Program
{
    class FruitComparer : ICompareThings<Fruit>
    { ... }
    static void Main()
    {
        // Allowed in C# 4.0 and later
        ICompareThings<Fruit> fc = new FruitComparer();
        Apple apple1 = new Apple();
        Apple apple2 = new Apple();
        Orange orange = new Orange();
        // A Fruit comparer can compare apples and oranges:
        bool b1 = fc.FirstIsBetter(apple1, orange);
        // or apples and apples:
        bool b2 = fc.FirstIsBetter(apple1, apple2);
        // This is legal because the interface is
        // contravariant
        ICompareThings<Apple> ac = fc;
        // This is really a Fruit comparer, so it can
        // still compare two apples
        bool b3 = ac.FirstIsBetter(apple1, apple2);
    }
}
```

Like covariance support, contravariance uses a type parameter modifier: in, which appears in the interface’s type parameter declaration. This instructs the compiler to check that T never appears on a property getter or as the return type of a method, thereby enabling contravariant conversions for this interface.

Contravariant conversions have all the analogous restrictions as described earlier for covariant conversions: They are valid only for generic interface and delegate types, the varying type arguments must be reference types, and the compiler must be able to verify that the interface is safe for the contravariant conversions.

An interface can be covariant in one type parameter and contravariant in another, but this seldom arises in practice except with delegates. The Func<A1, A2, . . . , R> family of delegates, for example, are covariant in the return type, R, and contravariant in all the argument types.