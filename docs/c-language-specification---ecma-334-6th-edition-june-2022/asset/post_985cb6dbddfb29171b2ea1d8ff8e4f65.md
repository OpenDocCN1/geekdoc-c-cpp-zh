
```csharp
{
    sum += selector(item);
}
return sum;
}
}
```

The `ItemList<T>` class has two `Sum` methods. Each takes a selector argument, which extracts the value to sum over from a list item. The extracted value can be either an `int` or a `double` and the resulting sum is likewise either an `int` or a `double`.

The `Sum` methods could for example be used to compute sums from a list of detail lines in an order.

```csharp
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}
```

```csharp
void ComputeSums()
{
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
    ...
}
```

In the first invocation of `orderDetails.Sum`, both `Sum` methods are applicable because the anonymous function `d => d.UnitCount` is compatible with both `Func<Detail,int>` and `Func<Detail,double>`. However, overload resolution picks the first `Sum` method because the conversion to `Func<Detail,int>` is better than the conversion to `Func<Detail,double>`.

In the second invocation of `orderDetails.Sum`, only the second `Sum` method is applicable because the anonymous function `d => d.UnitPrice * d.UnitCount` produces a value of type `double`. Thus, overload resolution picks the second `Sum` method for that invocation.

*end example*

## 11.16.5 Anonymous functions and dynamic binding

An anonymous function cannot be a receiver, argument, or operand of a dynamically bound operation.

## 11.16.6 Outer variables

### 11.16.6.1 General

Any local variable, value parameter, or parameter array whose scope includes the *lambda_expression* or *anonymous_method_expression* is called an **outer variable** of the anonymous function. In an instance function member of a class, this value is considered a value parameter and is an *outer variable* of any anonymous function contained within the function member.

### 11.16.6.2 Captured outer variables

When an outer variable is referenced by an anonymous function, the outer variable is said to have been **captured** by the anonymous function. Ordinarily, the lifetime of a local variable is limited to execution of the block or statement with which it is associated (§9.2.8). However, the lifetime of a captured outer variable is extended at least until the delegate or expression tree created from the anonymous function becomes eligible for garbage collection.

Example: In the example

```
using System;

delegate int D();

class Test
{
    static D F()
    {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main()
    {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```

the local variable x is captured by the anonymous function, and the lifetime of x is extended at least until the delegate returned from F becomes eligible for garbage collection. Since each invocation of the anonymous function operates on the same instance of x, the output of the example is:

1
2
3

end example

When a local variable or a value parameter is captured by an anonymous function, the local variable or parameter is no longer considered to be a fixed variable (§22.4), but is instead considered to be a moveable variable. However, captured outer variables cannot be used in a fixed statement (§22.7), so the address of a captured outer variable cannot be taken.

> Note: Unlike an uncaptured variable, a captured local variable can be simultaneously exposed to multiple threads of execution. end note

### 11.16.6.3 Instantiation of local variables

A local variable is considered to be instantiated when execution enters the scope of the variable.

Example: For example, when the following method is invoked, the local variable x is instantiated and initialized three times—once for each iteration of the loop.

```
static void F()
{
    for (int i = 0; i < 3; i++)
    {
        int x = i * 2 + 1;
        ...
    }
}
```

```
int x;
for (int i = 0; i < 3; i++)
{
    x = i * 2 + 1;
    result[i] = () => Console.WriteLine(x);
}
return result;
}
```

the output is:

5
5
5

Note that the compiler is permitted (but not required) to optimize the three instantiations into a single delegate instance (§10.7.2).

*end example*

If a for-loop declares an iteration variable, that variable itself is considered to be declared outside of the loop.

*Example:* Thus, if the example is changed to capture the iteration variable itself:

```
static D[] F()
{
    D[] result = new D[3];
    for (int i = 0; i < 3; i++)
    {
        result[i] = () => Console.WriteLine(i);
    }
    return result;
}
```

only one instance of the iteration variable is captured, which produces the output:

3
3
3

*end example*

It is possible for anonymous function delegates to share some captured variables yet have separate instances of others.

*Example:* For example, if F is changed to

```
static D[] F()
{
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++)
    {
        int y = 0;
        result[i] = () => Console.WriteLine($"{+x} {+y}");
    }
    return result;
}
```

the three delegates capture the same instance of *x* but separate instances of *y*, and the output is:

```
1 1
2 1
3 1
```

*end example*

Separate anonymous functions can capture the same instance of an outer variable.

*Example:* In the example:

```csharp
using System;

delegate void Setter(int value);
delegate int Getter();

class Test
{
    static void Main()
    {
        int x = 0;
        Setter s = (int value) => x = value;
        Getter g = () => x;
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```

the two anonymous functions capture the same instance of the local variable x, and they can thus “communicate” through that variable. The output of the example is:

```
5
10
```

*end example*

## 11.16.7 Evaluation of anonymous function expressions

An anonymous function *F* shall always be converted to a delegate type *D* or an expression-tree type *E*, either directly or through the execution of a delegate creation expression `new D(F)`. This conversion determines the result of the anonymous function, as described in §10.7.

## 11.16.8 Implementation Example

**This subclause is informative.**

This subclause describes a possible implementation of anonymous function conversions in terms of other C# constructs. The implementation described here is based on the same principles used by a commercial C# compiler, but it is by no means a mandated implementation, nor is it the only one possible. It only briefly mentions conversions to expression trees, as their exact semantics are outside the scope of this specification.

The remainder of this subclause gives several examples of code that contains anonymous functions with different characteristics. For each example, a corresponding translation to code that uses only other C# constructs is provided. In the examples, the identifier D is assumed to represent the following delegate type:

```
public delegate void D();
```

The simplest form of an anonymous function is one that captures no outer variables:

```
class Test
{
    static void F()
    {
        D d = () => Console.WriteLine("test");
    }
}
```

This can be translated to a delegate instantiation that references a compiler generated static method in which the code of the anonymous function is placed:

```
class Test
{
    static void F()
    {
        D d = new D(__Method1);
    }

    static void __Method1()
    {
        Console.WriteLine("test");
    }
}
```

In the following example, the anonymous function references instance members of this:

```
class Test
{
    int x;

    void F()
    {
        D d = () => Console.WriteLine(x);
    }
}
```

This can be translated to a compiler generated instance method containing the code of the anonymous function:

```
class Test
{
    int x;

    void F()
    {
        D d = new D(__Method1);
    }

    void __Method1()
    {
        Console.WriteLine(x);
    }
}
```
