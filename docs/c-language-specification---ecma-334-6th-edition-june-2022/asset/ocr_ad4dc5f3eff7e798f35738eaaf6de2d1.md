the three delegates capture the same instance of *x* but separate instances of *y*, and the output is:

```
```
1 1
2 1
3 1
```
```

*end example*

Separate anonymous functions can capture the same instance of an outer variable.

*Example:* In the example:

```
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
```

the two anonymous functions capture the same instance of the local variable x, and they can thus “communicate” through that variable. The output of the example is:

```
```
5
10
```
```

*end example*

# ## 11.16.7 Evaluation of anonymous function expressions

An anonymous function *F* shall always be converted to a delegate type *D* or an expression-tree type *E*, either directly or through the execution of a delegate creation expression `new D(F)`. This conversion determines the result of the anonymous function, as described in §10.7.

# ## 11.16.8 Implementation Example

**This subclause is informative.**

This subclause describes a possible implementation of anonymous function conversions in terms of other C# constructs. The implementation described here is based on the same principles used by a commercial C# compiler, but it is by no means a mandated implementation, nor is it the only one possible. It only briefly mentions conversions to expression trees, as their exact semantics are outside the scope of this specification.

The remainder of this subclause gives several examples of code that contains anonymous functions with different characteristics. For each example, a corresponding translation to code that uses only other