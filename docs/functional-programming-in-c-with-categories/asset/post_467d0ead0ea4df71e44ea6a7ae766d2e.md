
## 1.10 Using static directive

With the static directives one can use static methods without referring to the class. For example, because `WriteLine` is a `static` method of the `System.Console`

We can directly write:

```
WriteLine("message");
```

Instead of:

```
Console.WriteLine("message");
```

If we put as a using statement the following

```
using static System.Console;
```

like this:

```
using static System.Console;

namespace PracticalCSharp
{
    public class Demo
    {
        public void Run()
        {
            WriteLine("message");
        }
    }
}
```

In functional programming (and in language-ext) library we can use this to provide factory methods and avoid using the `new` keyword. For example, imagine that we have this class:

```
public class IO<T>
{
    public Func<T> Fn { get; set; }
    public IO(Func<T> fn) => Fn = fn;
    public T Run() => Fn();
}
```

Instead of writing:

```
var t = new IO(() => 1);
```

We can define a class with a static method that creates `new IO()`

```
public class Factories
{
    public static IO<T> IO<T>(Func<T> fn) => new IO<T>(fn);
```

In this way by using static Factories we can write directly:

```
var t = IO(() => 1);
```

Without the new keyword. We can argue about the usefulness of this idea. But it is a tradition coming from functional languages and minimizes the syntax. Also allows us to hide the new inside a single point. In this way if we wanted to change the class that is created on every IO(() => ...) function call, we only have to change the static definition, like we do when we use the standard factory design pattern, or an IoC container.

In language-ext library most of the Types have static “factories”, so we can usually write expressions like the following:

```
var optional = Some(123);
```

Instead of :

```
var optional = new Some(123);
```

## 1.11 LINQ support for custom Data structures

Did you know that if you implement Select method in any type you can use the from... in ...select Linq syntax??? The C# community quickly saw in this LINQ feature a way to emulate a syntactic pattern for chaining computation called Do notation looks something like this in Haskell:

```
do { x1 <- action1
  ; x2 <- action2
  ; action( x1,x2 )}
```

This would translate to something like this in LINQ

```
var r = from x1 in new Id<int>(5)
    from x2 in new Id<int>(2)
    select x1 + x2;
```

we will see the way to add Linq support for custom data structures in more detail in the Functors and Monads Chapters. We also can use extension methods to provide LINQ support for native C# types like Lazy<T> for example:

```
public static Lazy<T1> Select<T, T1>(this Lazy<T> @this, ...) =>{ ... }
```

that would allow for something like this:

```
var r = from x1 in new Lazy <int>(( )=>5)
    select x1 + 1;
```

## 1.12 Currying and partial application

Currying is a considerably basic and profound concept in functional programming. That is why it carries the name of the great Haskell Curry. Currying means that a function that takes multiple arguments can be translated into a series of function calls that each take a single argument. An expression like this:

```
public string F(int x, int y) { }
```

that we invoke like this

```
var resultString = F(4,5);
```

can be transformed to the equivalent :

```
public Func<int, string> F(int x)
{
    string g(int y) { }
    return g;
}
```

Which we can call like this:

```
var resultString = F(4)(5);
```

or if we just use lambda the previous transformation would look like this:

```
Func<int, int, string> F = (x, y) => { };
```

```
Func<int, Func<int, string>> F1 = x => y => { };
```

We say that the second is the Curried version of the first. I know that using Func delegates it makes it difficult to grasp. For example, in JavaScript where we don’t have types the previous looks like this:

```
var f = (x, y, z) => {...}
```

```
var f = x=>y=>z=> {...}
```

we replace the commas ( , ) with arrows =>.

The language-ext library provides Currying functions. A simple implementation of a generic Higher-order function that transforms a two-argument function, into its curried version looks like this:

```
Func<A, Func<B, C>> Curry<A, B, C>(Func<A, B, C> f) => (A x)=>(B y) => f(x, y);
```

the type of this function is ((A × B) → C) →(A →(B →C)). In a more specific example, a function that has a discount and a price argument:

```
Func<double, double, double> discountedPrice = (discount, price) =>
```

```
price - discount * price;
```

the equivalent curried function would look like this:

```
Func<double, Func< double, double>> discountedPrice = (discount) => (price) =>
    price - discount * price;
```

If we wanted to use the un-curried function with an array of prices, using a given discount normally one would write:

```
var discountedPrices = new List<double> { 10, 20, 30 }
    .Select(x =>discountedPrice(0.1, x));
```

here is the curried version:

```
var discountedPrices1 =new List<double>{ 10, 20, 30 }
    .Select(discountedPriceCurried(0.1));
```

The difference here is that in the second case, we do not have the .Select(x => because there is no need to refer to the array object explicitly. For this reason, the first style of writing is called pointed and the second one point free.

After we fixed an argument to a specific discount 0.1 we got a specialized function:

```
var discountedPricePartial = x => discountedPrice(0.1, x);
```

this process of reducing the arguments of a function it is called partial application, (or sometimes we might refer to this process as a specialization) and is usually mentioned alongside with currying, because after currying a function, we can get a partial application on the fly like this :

```
Curry(discountedPrice)(0.1)
```

### Partial Application

Partial application is a very simple concept to understand. Lets say we have a two-argument function:

```
R F<A, B, R>(A a, B b) => default(R);
```

We can create a new function:

```
R G<B, R>(B b) => F<A, B, R>(x1, b);
```

That takes a single argument by providing some default value x1 for the A argument.

![](img/d73681d801b4b826e0b2a293897bbba4_44_0.png)

As a simple example consider the predicate, that tests if two integers are equal:

```
bool areEqual(int a, int b = 0) => a == b;
```

we can create a range of specialized predicates by partial applying on any of the arguments:

```
bool isZero(int a) => areEqual(a, 0);
```

```
bool isOne(int a) => areEqual(a, 1);
```

![](img/d73681d801b4b826e0b2a293897bbba4_45_0.png)

obviously, we can partially apply values to more than one argument (or even all of them )

![](img/d73681d801b4b826e0b2a293897bbba4_45_1.png)

currying always leaves the function at hand in the same syntactical state of x=>y=>z=>... every time we use **compose** or **partially apply** a value, we consume an arrow (=>), but the result maintained the same syntactical form; y=>z=>... thus promoting uniformity. This is idempotent design in practice. The downside is that the order of arguments becomes now important, and simple reorder refactoring of arguments might have side effects.

## Algebras of Programming

Category Theory is a mathematical discipline with a wide range of applications in theoretical computer science. Concepts like Category, Functor, Monad, and others, which were originally defined in Category Theory, have become pivotal for the understanding of modern Functional Programming (FP) languages and paradigms.

The Category is just an extension of the classical notion of Set of Objects. A category C consists of the following three mathematical entities:

+   1. A class ob(C), whose elements are called objects. Any object-oriented programmer would find this as a great way to start a definition.

![](img/d73681d801b4b826e0b2a293897bbba4_46_0.png)

Our favorite category in programming is the category of types int, bool, char, etc. There are many interesting categories in programming and in this book, we will explore some of them.

![](img/d73681d801b4b826e0b2a293897bbba4_46_1.png)
