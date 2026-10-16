
在编程语言理论和证明论中，柯里-霍华德对应（Curry-Howard correspondence）描述的是计算机程序与数学证明之间的直接关系。我们会在后续内容中探讨其中的一些联系。在本书范围内，我们只以简化的方式粗略地介绍一下柯里-霍华德对应。

第一个明确的联系是 `λ` 抽象（`⇒`）与逻辑蕴含（`→`）之间的对应：

类型 | 逻辑

引入 | `[x:A]¹ ... M:B / λx.M: A → B ⇒ I₁` | `[A]ˣ ... B / A → B ⇒ I₁`

消去 | `λx.M: A → B   t:A / M(t): B ⇒ E` | `A → B   A / B → E`

+   1. 一条引入规则，描述如何创建该类型的元素；

+   2. 一条消去规则，描述如何使用该类型的元素。

对应关系如下：

+   1. 逻辑中的蕴含引入类似于 `λ` 演算中的 `λ` 抽象。

+   2. 逻辑中的蕴含消去类似于 `λ` 演算中的 `λ` 应用。

我们最容易证明的是恒等函数：`Func<A, A> Id = (A x) => x;`

逻辑

`[A]^x`

---

`A → A  → I_x`

类型

`[x: A]`

---

`λx. x: A → A  ⇒ I_x`

自然演绎推导十分简单：

+   1. `[A]^x`：我们做出一个假设 `[A]^x`，即我们有一个 `A`。在代码中，这意味着我们以 `(A x) =>` 开始 lambda，于是我们就被赋予了一个 `A`，可以在函数实现中使用它。问题是，当我们需要使用 `Id` 时，必须有一个 `A` 可用。在演绎上下文中，`[...]^x` 这种记号被用作簿记机制，以追踪假设。

+   2. 然后立即得出结论 `A`（即 `(A x) => x`），并通过调用蕴含 `→` 引入规则来消去假设（撤销假设）`[A]^x`。

另一个简单的重言式是命题 `A → (B → A)` [这被称为 `K` 组合子]，下面是用 C# 仅通过 lambda 给出的直接实现：

```
Func<A, Func<B, A>> K = (A x) => ((B y) => x);
```

它对应于如下 `λ` 项：

`λx:A. λy:B. x: (A → (B → A))`

`K` 只是接受一个变量 `x:A`，返回一个函数；该函数接受 `y:B` 但完全忽略它，并返回最初的变量 `x`。是的，正如你可能预料到的，它在实际场景中完全无用。

为了完整地介绍组合子，我们还会简要讨论 `S` 组合子。

```
Func<Func<A, B>, Func<A, C>> S<A, B, C>(Func<A, Func<B, C>> f) =>
    (Func<A, B> g) => ((A a) => f(a)(g(a)));
```

这个函数的类型是：

`S: (A → (B → C)) → ((A → B) → (A → C))`

And it is an interesting exercise to try and implement `S` in C# because it will give you better understanding of `Func` delegates.

`S`, takes `x` and applies it to both `f` and `g` and then applies the `g(x)` onto `f(x)`. We will find this in the applicative reader functor section. The `x` should be understood like a common environment of variables (or a configuration) that is provided to both `f` and `g`, and then we apply the result of `g(x)` to the `f(x)`, which is a function. An example would be the following:

```
Product result = S<Config,Product,Product>
(config =>product=>new Product(product.Name, product.Price*(1- config.Discount)))
(config => new Product($"A:{config.Category}", 100))
(new Config(0.1, "Widgets"));
```

We used the Combinator to pass (1) the `Config(0.1, "Widgets")` to the first lambda (2) and create a new `Product` and then we passed both the configuration and the `Product` to the (3) lambda to create a discounted `Product` using the `Config` Discount.

### η-reduction / expansion - Point Free notation

Let us say we have a simple lambda:

```
Func<int, int> f = (int a) => a + 1;
```

We can use this directly in any method that accepts a `Func<int, int>` delegate:

```
var x = new List<int> { 1, 2, 3 }.Select(f);
```

but we can also create a new lambda that explicitly call the function:

```
var y = new List<int> { 1, 2, 3 }.Select(x => f(x));
```

this is an `η`-expansion (eta-expansion). It is obvious that `f ≡ (x => f(x))`, that is the function `f` is equivalent to the lambda `x => f(x)`. We can also keep doing this process indefinitely for example we could define the following lambdas:

```
Func<int, int> f1 = (int x) => f(x);
```

```
Func<int, int> f2 = (int x) => f1(x);
```

Each of which can be used in place of the initial `f` e.g.:

```
var z = new List<int> { 1, 2, 3 }.Select(f1);
```

when we move in the opposite direction by simplifying a `x => f(x)` into just `f`, we make what is called an `η`-reduction (eta-reduction)

```
new List<int> { 1, 2, 3 }.Select(x => f(x));
```

![](img/d73681d801b4b826e0b2a293897bbba4_24_0.png)

```
new List<int> { 1, 2, 3 }.Select(f);
```

this syntax is called `point-free` because you don’t have explicit reference to the object `x =>`

> That is called the “point”

```
new List<int> { 1, 2, 3 }.Select(x => f(x));
```

The formal justification from `Gentzen` is that the introduction for lambda `(int x)=>` is (post)-inverse to the lambda elimination `f(x)`

![](img/d73681d801b4b826e0b2a293897bbba4_24_1.png)

```
Func<int, int> f1 = (int x) => f(x);
```

In the logical form we just conclude `B` from `A` and `(A → B)` and then immediately introduce the assumption of `A` getting back the `(A → B)`

![](img/d73681d801b4b826e0b2a293897bbba4_24_2.png)

or in type theoretic derivation

![](img/d73681d801b4b826e0b2a293897bbba4_24_3.png)

### 1.5 Higher-order functions

A `Higher-Order function (Hof)` is a function that receives a function as an argument or returns a function as output. But I assume that you are already familiar with this definition.

The following is a `Hof` because it takes a `Func<T, U>` delegate as an argument.

```
R F<T, U, R>(Func<T, U> g, T y)
{
    ...
}
```

The type of this function is `F: ((T→U) × T) → R`. While the following is a `Hof` because it returns a `Func<T, U>`

```
Func<T, U> G<T, U>(T y)
{
    ...
}
```

With a type of `G: T→(T→U)`, we can also use the local function form inside other methods or functions.

In the form of `Func` delegates the previous functions now should be declared like this:

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

Again, here the type of `Func<Func<T, U>, T, R>` corresponds to `((T→U) × T) →R` and the type of `Func<T, Func<T, U>>` corresponds to `T→(T→U)`

Obviously, we can have as many levels of Higher order Functions by allowing the Functions passed as arguments or return as results being themselves of Higher type. For example:

```
R F<T, U, R>(Func<Func<T, U>, U> g, T y)
{
    ...
}
```

This is a `Hof` passed as an argument.

With type `F: (((T→U) →U) × T) →R`. In practice this type of Higher-Higher-order-functions becomes too convoluted too fast, and it is not recommended. In a delegate variable declaration this already looks way to complex.

```
Func<Func<Func<T, U>, U>, T, R> F = (Func<Func<T, U>, U> g, T y) => ...
```

What makes it worse is that we cannot replace the variable type with the `var` keyword.

### Strategy design pattern

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

If we have defined an `Order` class, responsible for handling a collection of `Product` items, we can place there the calculation of the Total amount, by using a `IDiscountStrategy` that might vary:

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

In his way if we have an order containing some `Products`, we can instruct how the discount will be computed by providing at run time a concrete class implementing `IDiscountStrategy`

```
var total = order.GetTotalPrice(new PremiumDiscountStrategy());
```
