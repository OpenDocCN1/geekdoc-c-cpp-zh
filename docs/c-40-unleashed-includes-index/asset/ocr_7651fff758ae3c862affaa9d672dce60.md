# # Lambda Expressions

With the advent of LINQ in C# 3.0 the use of functions as arguments to higher-order query operator functions was to become a day-to-day activity for developers, having to write query expressions like the following:

```
```csharp
int[] numbers = new [] { 1, 2, 3, 4, 5 };
var evens = numbers.Where(delegate (int i) { return i % 2 == 0; });
var odds  = numbers.Where(delegate (int i) { return i % 2 != 0; });
```
```

You will agree that the preceding code is still quite overloaded with syntactical noise that comes from the use of anonymous function expressions: delegates, returns, curly braces.

> > **NOTE**
> > Simplified query expression syntax exists in C# 3.0, reducing the need to deal with the query operator functions directly. However, in various cases, no such syntax exists, requiring users to pass functions manually as shown earlier. This makes it a worthy goal to make anonymous function expressions easier on the eye.

Lambda expressions are yet another simplification on top of delegate instantiation, also allowing inline declaration of functions (with support for closures) but in a more compact way. The two preceding calls can be simplified as follows:

```
```csharp
int[] numbers = new [] { 1, 2, 3, 4, 5 };
var evens = numbers.Where((int i) => i % 2 == 0);
var odds  = numbers.Where((int i) => i % 2 != 0);
```
```

The lambda arrow token => can be read as “goes to.” For example, “An integer value i goes to the Boolean expressing whether the integer value is divisible by 2.” In fact, given the signature of Where and the type of numbers, the compiler can infer the type of the lambda argument:

```
```csharp
IEnumerable<T> Where<T>(this IEnumerable<T> source, Func<T, bool> predicate);
```
```

Because source is an IEnumerable<int>, T has to be int, and therefore the input to the predicate has to be of the same type. This allows us to simplify the syntax even further, also dropping the parentheses around i:

```
```csharp
int[] numbers = new [] { 1, 2, 3, 4, 5 };
var evens = numbers.Where(i => i % 2 == 0);
var odds  = numbers.Where(i => i % 2 != 0);
```
```