```
```csharp
object baseObject = new object();
Currency derivedCopy1 = (Currency)derivedObject;    // OK
Currency derivedCopy2 = (Currency)baseObject;       // Exception
thrown
```
```

This code works in a way similar to the code presented earlier for reference types. Casting `derivedObject` to `Currency` works fine because `derivedObject` actually refers to a boxed `Currency` instance—the cast is performed by copying the fields out of the boxed `Currency` object into a new `Currency` struct. The second cast fails because `baseObject` does not refer to a boxed `Currency` object.

When using boxing and unboxing, it is important to understand that both processes actually copy the data into the new boxed or unboxed object. Hence, manipulations on the boxed object, for example, do not affect the contents of the original value type.

# Multiple Casting

One thing you have to watch for when you are defining casts is that if the C# compiler is presented with a situation in which no direct cast is available to perform a requested conversion, it attempts to find a way of combining casts to do the conversion. For example, with the `Currency` struct, suppose the compiler encounters a few lines of code like this:

```
```csharp
var balance = new Currency(10,50);
long amount = (long)balance;
double amountD = balance;
```
```

You first initialize a `Currency` instance, and then you attempt to convert it to a `long`. The trouble is that you haven’t defined the cast to do that. However, this code still compiles successfully. Here’s what happens: The compiler realizes that you have defined an implicit cast to get from `Currency` to `float`, and the compiler already knows how to explicitly cast a `float` to a `long`. Hence, it compiles that line of code into IL code that converts `balance` first to a `float`, and then converts that result to a `long`. The same thing happens in the final line of the code, when you convert `balance` to a `double`. However, because the cast from `Currency` to `float` and the predefined cast from `float` to `double` are both implicit, you can write this conversion in your code as an implicit cast. If you prefer, you could also specify the casting route explicitly:

```
```csharp
var balance = new Currency(10,50);
long amount = (long)(float)balance;
double amountD = (double)(float)balance;
```
```

However, in most cases, this would be seen as needlessly complicating your code. The following code, by contrast, produces a compilation error:

```
```csharp
var balance = new Currency(10,50);
long amount = balance;
```
```

The reason is that the best match for the conversion that the compiler can find is still to convert first to `float` and then to `long`. The