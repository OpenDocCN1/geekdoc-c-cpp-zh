
And it is an interesting exercise to try and implement S in C# because it will give you better understanding of Func delegates.

S, takes x and applies it to both f and g and then applies the g(x) onto f(x). We will find this in the applicative reader functor section. The x should be understood like a common environment of variables (or a configuration) that is provided to both f and g, and then we apply the result of g(x) to the f(x), which is a function. An example would be the following:

```
Product result = S<Config,Product,Product>
(config =>product=>new Product(product.Name, product.Price*(1- config.Discount)))
(config => new Product($"A:{config.Category}", 100))
(new Config(0.1, "Widgets"));
```

We used the Combinator to pass (1) the Config(0.1, "Widgets") to the first lambda (2) and create a new Product and then we passed both the configuration and the Product to the (3) lambda to create a discounted Product using the Config Discount.

## η-reduction / expansion - Point Free notation

Let us say we have a simple lambda:

```
Func<int, int> f = (int a) => a + 1;
```

We can use this directly in any method that accepts a Func<int, int> delegate:

```
var x = new List<int> { 1, 2, 3 }.Select(f);
```

but we can also create a new lambda that explicitly call the function:

```
var y = new List<int> { 1, 2, 3 }.Select(x => f(x));
```

this is an η-expansion (eta-expansion). It is obvious that f ≡ (x => f(x)), that is the function f is equivalent to the lambda x => f(x). We can also keep doing this process indefinitely for example we could define the following lambdas:

```
Func<int, int> f1 = (int x) => f(x);
```

```
Func<int, int> f2 = (int x) => f1(x);
```

Each of which can be used in place of the initial f e.g.:

```
var z = new List<int> { 1, 2, 3 }.Select(f1);
```

when we move in the opposite direction by simplifying a **x => f(x)** into just **f**, we make what is called an **η-reduction (eta-reduction)**

```
new List<int> { 1, 2, 3 }.Select(x => f(x));
```

![](img/d73681d801b4b826e0b2a293897bbba4_24_0.png)

```
new List<int> { 1, 2, 3 }.Select(f);
```

this syntax is called _point-free_ because you don’t have explicit reference to the object **x =>**

> That is called the “point”

```
new List<int> { 1, 2, 3 }.Select(x => f(x));
```

The formal justification from _Gentzen_ is that the introduction for lambda `(int x)=>` is (post)-inverse to the lambda elimination `f(x)`

![](img/d73681d801b4b826e0b2a293897bbba4_24_1.png)

```
Func<int, int> f1 = (int x) => f(x);
```

In the logical form we just conclude **B** from **A** and **(A → B)** and then immediately introduce the assumption of **A** getting back the **(A → B)**

![](img/d73681d801b4b826e0b2a293897bbba4_24_2.png)

or in type theoretic derivation

![](img/d73681d801b4b826e0b2a293897bbba4_24_3.png)

## 1.5 Higher-order functions

A **Higher-Order function (Hof)** is a function that receives a function as an argument or returns a function as output. But I assume that you are already familiar with this definition.

The following is a Hof because it takes a Func<T, U> delegate as an argument.

```
R F<T, U, R>(Func<T, U> g, T y)
{
    ...
}
```

The type of this function is **F: ((T→U) × T) → R**. While the following is a Hof because it returns a Func<T, U>

```
Func<T, U> G<T, U>(T y)
{
    ...
}
```

With a type of **G: T→(T→U)**, we can also use the local function form inside other methods or functions.

In the form of Func delegates the previous functions now should be declared like this:

```
Func<Func<T, U>, T, R> F = (Func<T, U> g, T y) => ...
```

```
Func<T, Func<T, U>> G = (T y) => ...
```

unfortunately, C# does not allow for Generic definitions at the level of the delegate. We cannot write for example :

```
Func<Func<T, U>, T, R> F = <T, U, R>(Func<T, U> g, T y) => ...
```

```
Func<T, Func<T, U>> G = <T, U>(T y) => ...
```

For this reason, we must place them in a Function or Class, and include the generic constrains there:

```
public static void Foo<T, U, R>()
{
    Func<Func<T, U>, T, R> F = (Func<T, U> g, T y) => ...
```

```
Func<T, Func<T, U>> G = (T y) => ...
}
```

Again, here the type of Func<Func<T, U>, T, R> corresponds to ((T→U) × T) →R and the type of Func<T, Func<T, U>> corresponds to T→(T→U)

Obviously, we can have as many levels of Higher order Functions by allowing the Functions passed as arguments or return as results being themselves of Higher type. For example:

```
R F<T, U, R>(Func<Func<T, U>, U> g, T y)
{
    ...
}
```

This is a Hof passed as an argument.

With type F: (((T→U) →U) × T) →R. In practice this type of Higher-Higher-order-functions becomes too convoluted too fast, and it is not recommended. In a delegate variable declaration this already looks way to complex.

```
Func<Func<Func<T, U>, U>, T, R> F = (Func<Func<T, U>, U> g, T y) => ...
```

What makes it worse is that we cannot replace the variable type with the var keyword.

## Strategy design pattern

The strategy design pattern is the closest thing to Higher order function form a purely OOP perspective since it allows to pass around functions as Objects. With the strategy pattern, we can modify the behavior of an object based on the different strategy object that we pass to it.

If for example, we have two different discounting scenarios for our product, we can abstract the discounting calculation from the product object and place it in a strategy object.

![](img/d73681d801b4b826e0b2a293897bbba4_26_0.png)

```
public interface IDiscountStrategy {
    double GetDiscountedPrice(Product product);
}
```

```
public class PremiumDiscountStrategy : IDiscountStrategy {
    public double GetDiscountedPrice(Product product) => product.Price * 0.7;
}
```

```
public class BasicDiscountStrategy : IDiscountStrategy {
    public double GetDiscountedPrice(Product product) => product.Price * 0.9;
}
```

If we have defined an Order class, responsible for handling a collection of Product items, we can place there the calculation of the Total amount, by using a IDiscountStrategy that might vary:

```
public class Order
{
    IList<Product> Products { get; }

    public Order(IList<Product> products) => Products = products;

    public double GetTotalPrice(IDiscountStrategy activeDiscount) =>
        Products
            .Select(activeDiscount.GetDiscountedPrice)
            .Sum();
}
```

In his way if we have an order containing some Products, we can instruct how the discount will be computed by providing at run time a concrete class implementing IDiscountStrategy

```
var total = order.GetTotalPrice(new PremiumDiscountStrategy());
```

In a functional manner we could refactor this to directly pass the discount calculation function Func<Product, double> as an argument. We can thus define a GetTotalPrice function:

```
double GetTotalPrice(List<Product> products, Func<Product, double> activeDiscount) =>
    products.Select(activeDiscount).Sum();
```

and define some predetermined Discounts:

```
Func<Product, double> PremiumDiscountStrategy = (Product product) =>
    product.Price * 0.7;
```

```
Func<Product, double> BasicDiscountStrategy = (Product product) =>
    product.Price * 0.9;
```

We could even define the GetDiscountedPrice function, as an extension method attached on the List<Product> type:

```
public static partial class FunctionalExtensions
{
    public static double GetDiscountedPrice(this List<Product> @products,
        Func<Product, double> activeDiscount) =>
        products.Select(activeDiscount).Sum();
}
```

This would allow for the following syntax:

```
var total = products.GetDiscountedPrice(PrimumDiscountStrategy);
```

In this example GetDiscountedPrice(...) is the Higher-order Function. We can call this refactoring move “Replace Strategy with Higher-order Function.” For simple scenarios, we do not have to create a full class in order to use the strategy pattern. In functional programming Higher-order functions are everywhere. This is the core idea of functional programming; to treat functions as data.

## 1.6 Simple Function Composition

One can argue that composing functions is the most important idea in programming and functional programming in particular. Functional composition is an instance of the concept of compositionality. Creating systems by composing smaller systems that are easier to implement and design can be found in all levels of programming. Staring from the Syntax of the language, to Design patterns, architectural patterns, larger System design etc.

In this section we are going to take a brief look at one of the most basic ones; Function composition.

In mathematics, function composition is the application of one function to the result of another to produce a third function. For instance, the functions f : T→ R and g : R→ U can be composed to yield a function h: g(f(x)) with type T→ U we usually represent that as g ∘ f and we read that as “g after f” the symbol ∘ usually represents “after”.

![](img/d73681d801b4b826e0b2a293897bbba4_28_0.png)

```
Func<T, R> Compose<T, U, R>(Func<T, U> f, Func<U, R> g) => (T x) => g(f(x));
```
