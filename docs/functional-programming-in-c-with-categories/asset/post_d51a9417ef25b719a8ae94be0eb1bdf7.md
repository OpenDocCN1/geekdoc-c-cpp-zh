
```csharp
Func<double> ProductA = () => 100;
Func<double> ProductB = () => 200;
Func<Func<double>, Func<double>> Packaging =
    (product) => () => product() + 10;

Func<double> packagedProduct = Packaging(ProductA);
```

So, in a way any function of this form `(T a) => (R b) => {}` is equivalent to an object that takes an `a: T` in the constructor and has only one method that takes a `b: R` as argument.

Only functions: `(Func<double> product) => () => {...}`
OOP: `class Packaging { constructor(IPriced product) {...} double getPrice() {...} }`

The idea here is for the decorating composing functions that come after the decorated function that has a return type Product.

![](img/d73681d801b4b826e0b2a293897bbba4_61_0.png)

## Tuple notation

Another way to represent the Object is to use tuples. Unfortunately C# does not allow Tuples with only a single member. So, for presentation purposes we add another method to our product that returns the name `getName: () => name`. Now we can define a product by a function that acts as a Constructor:

```csharp
Func<string, double, (Func<string> getName, Func<double> getPrice)> Product =
    (string name, double price) =>
        (getName: () => name, getPrice: () => price);
```

We can use this in order to create products:

![](img/d73681d801b4b826e0b2a293897bbba4_61_1.png)

```csharp
(Func<string> getName, Func<double> getPrice) ProductA = Product("A", 100);
(Func<string> getName, Func<double> getPrice) ProductB = Product("B", 200);
```

Now we can define the Decorator function as follows:

```csharp
Func<(Func<string> getName, Func<double> getPrice),
    (Func<string> getName, Func<double> getPrice)>
    Packaging =
    product =>
    (
        getName: () => product.getName() + "Packaging",
        getPrice: () => product.getPrice() + 0.1
    );
```

Which then we can use like this:

```csharp
(Func<string> getName, Func<double> getPrice) packagedProduct = Packaging(ProductA);
```

```csharp
(Func<string> getName, Func<double> getPrice) doublePackagedProduct = Packaging(Packaging(ProductA));
```

Obviously the Tuples as Object minimal syntax here is only for presentation purposes. In C# 9.0 immutable record types have been added in order to cover the cases where we want to adhere to a more minimal functional coding style.

## 2.8 Predicate Monoidal Composition

The most famous contravariant functional type is the Predicate, which is any function that has a type of `_ → bool` (returns a Boolean). We already saw that .NET provides a native Predicate delegate:

```csharp
public delegate bool Predicate<in T>(T obj);
```

In practice we usually use the delegate `Func<T, bool>` to represent predicates. Most of the .NET framework internally also uses `Func<T, bool>` as the predicate type. For example, the .NET framework definition for `List<T>.Where` has the following signature:

```csharp
IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate)
```

### Category Theory: Contravariant Types

Those kinds of types are called contravariant because they have the "changing (Type)" in the "negative side of the function (which is the input)". The input argument is what varies `(T x) → bool`. When we say here that the input argument varies, we mean that the Type of the input argument is generic (we have parametric polymorphism on the input argument), whereas the return type is fixed to `bool`.

To understand why it's contravariant, try to compose a function `T → R` with a predicate `(R a) => bool` to get a predicate `(T a) => bool`. The only way to have a composition is to pre-compose the `T → R` to the `(R a) => bool` to get a `(T a) => bool`.

![](img/d73681d801b4b826e0b2a293897bbba4_63_0.png)

This visually looks like this:

`T → R ∘ R → ● ⇔ T → ●`

Where `●` is the `bool` in our case.

In this way for the Predicate, we can define a PreCompose function:

```csharp
Predicate<R> PreCompose<T, R>(Func<R, T> f, Predicate<T> g) => (R x) => g(f(x));
```

The whole contravariant pre-composition becomes obvious when you take a look at this simple example where we have a `Predicate<double>` on the Price and we want to produce a `Predicate<Product>` on the Product using a Projection for the Price GetPrice:

```csharp
Predicate<double> IsHighPriced = (price) => price > 100;
```

```csharp
Func<Product, double> GetPrice = (product) => product.Price;
```

```csharp
Predicate<Product> IsHighPricedProduct = PreCompose(GetPrice, IsHighPriced);
```

This is one way to compose contravariant types like Predicate.

Another way is the monoidal composition. Using the monoidal operations on the bool, `&&`, `||`, `~`, we can define various compositions `And`, `Or`, and `Not` that would allow us to form larger Predicates from simpler ones.

The specification design pattern is based on this idea by defining:

```csharp
Func<T, bool> And<T>(Func<T, bool> p1, Func<T, bool> p2) => (T x) => p1(x) && p2(x);
```

```csharp
Func<T, bool> Or<T>(Func<T, bool> p1, Func<T, bool> p2) => (T x) => p1(x) || p2(x);
```

```csharp
Func<T, bool> Not<T>(Func<T, bool> p1) => (T x) => !p1(x);
```

![](img/d73681d801b4b826e0b2a293897bbba4_64_0.png)

We can create a new predicate by just applying both predicates and then gluing their bool results.

Then we can use some elementary basic predicates on the product:

```csharp
Func<string, Func<Product, bool>> nameContains = pattern => product =>
    product.Name.Contains(pattern);
```

```csharp
Func<Product, bool> highPriced = product => product.Price > 1000;
```

and then we can compose them using `And`, `Or`, and `Not` to create more complex predicates like:

```csharp
Func<Product, bool> highPricedAndContainsA = And(highPriced, nameContains("A"));
```

We can use those predicates with the filter method of the array:

```csharp
var products = new List<Product>{
    new Product("widgetA", 100),
    new Product("widgetB", 1100),
    new Product("widgetA", 2000),
    new Product("widgetB", 300)
};
```

```csharp
var notHighPricedAndContainsA = Not(highPricedAndContainsA);
```

```csharp
var filteredProducts = products.Where(notHighPricedAndContainsA);
```

Run This: .NET Fiddle

or try filtering the List with the following Predicates

```csharp
var filter = Or(highPriced, nameContains("B"));
```

```csharp
var filter = Not(Or(highPriced, nameContains("B")));
```

We can further simplify the syntax by providing static extensions to allow for fluent composition:

```csharp
public static partial class FunctionalExt
{
    public static Func<T, bool> And<T>(this Func<T, bool> @this, Func<T, bool> p) =>
        (T x) => @this(x) && p(x);

    public static Func<T, bool> Not<T>(this Func<T, bool> @this) =>
        (T x) => !@this(x);
}
```

Now we can write:

```csharp
Func<Product, bool> notHighPricedAndContainsA = highPriced.And(nameContains("A")).Not();
```

## 2.9 Specification Pattern - Functional Perspective

We can extract those mechanics in a fluent building construction that allow us to create predicate expressions. This is the very famous Specification pattern. The specification pattern often invokes mixed reactions, and it is even considered as an anti-pattern by many. Nonetheless, it is a part of the Domain-Driven Design tactical patterns as envisioned by Eric Evans.

![](img/d73681d801b4b826e0b2a293897bbba4_65_0.png)

The basic idea for the specification pattern is the composition of Predicates over the Boolean monoid that we saw previously. The main object-oriented enhancement is the addition of a fluent builder that allows us to chain expressions that look like the following:

```csharp
var spec1 = new Spec(nameContains("A")).And(highPriced);
```

Instead of the "functional"

```csharp
And(highPriced, nameContains("A"))
```

the core is the CompositeSpecification from which all other expressions inherit:

```csharp
public interface ISpecification<T> {
    bool IsSatisfiedBy(T item);
}
```

// In order to add fluent builder semantics onto the And, Or, Not

```csharp
public abstract class CompositeSpecification<T> : ISpecification<T>
{
    public CompositeSpecification<T> And(ISpecification<T> spec) =>
        new And<T>(this, spec);
    public CompositeSpecification<T> Or(ISpecification<T> spec) =>
        new Or<T>(this, spec);
    public CompositeSpecification<T> Not() =>
        new Not<T>(this);
    public abstract bool IsSatisfiedBy(T item);
}
```

Here we are going to have a base `Spec<T>`:

```csharp
public class Spec<T> : CompositeSpecification<T>
{
    private Func<T, bool> expression;
    public Spec(Func<T, bool> expression) => this.expression = expression;
    public override bool IsSatisfiedBy(T item) => expression(item);
}
```

Take a look at the `And<T>`:

```csharp
public class And<T> : CompositeSpecification<T>
{
    private ISpecification<T> left;
    private ISpecification<T> right;
    public And(ISpecification<T> left, ISpecification<T> right)
    {
        this.left = left;
        this.right = right;
    }
    public override bool IsSatisfiedBy(T item) =>
        left.IsSatisfiedBy(item) && right.IsSatisfiedBy(item);
}
```

> CompositeSpecification provides a fluent interface.

Run This .NET Fiddle
