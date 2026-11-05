
The first assignment successfully converts the anonymous function to the delegate type Func<int, int> because, when x is given type int, x + 1 is a valid expression that is implicitly convertible to type int.

Likewise, the second assignment successfully converts the anonymous function to the delegate type Func<int, double> because the result of x + 1 (of type int) is implicitly convertible to type double.

However, the third assignment generates a compile-time error because, when x is given type double, the result of x + 1 (of type double) is not implicitly convertible to type int.

Anonymous functions may influence overload resolution and may participate in type inference. See §7.5 for further details.

## 6.5.1 Evaluation of Anonymous Function Conversions to Delegate Types

Conversion of an anonymous function to a delegate type produces a delegate instance that references the anonymous function and the (possibly empty) set of captured outer variables that are active at the time of the evaluation. When the delegate is invoked, the body of the anonymous function is executed. The code in the body is executed using the set of captured outer variables referenced by the delegate.

The invocation list of a delegate produced from an anonymous function contains a single entry. The exact target object and target method of the delegate are unspecified. In particular, it is unspecified whether the target object of the delegate is null, the this value of the enclosing function member, or some other object.

Conversions of semantically identical anonymous functions with the same (possibly empty) set of captured outer variable instances to the same delegate types are permitted (but not required) to return the same delegate instance. The term “semantically identical” is used here to mean that execution of the anonymous functions will, in all cases, produce the same effects given the same arguments. This rule permits code such as the following to be optimized.

```
delegate double Function(double x);
class Test
{
    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void F(double[] a, double[] b) {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

Since the two anonymous function delegates have the same (empty) set of captured outer variables, and since the anonymous functions are semantically identical, the compiler is permitted to have the delegates refer to the same target method. Indeed, the compiler is permitted to return the very same delegate instance from both anonymous function expressions.

> > **JON SKEET** This potential optimization is somewhat dangerous when one considers the prospect of combining and removing delegates—which is particularly important when it comes to events. Consider this piece of code:
> > ```csharp
> > button.Click += (sender, args) => Console.WriteLine("clicked");
> > button.Click -= (sender, args) => Console.WriteLine("clicked");
> > ```
> > Assuming a simple event implementation, what will be the result? Either the button's click event will have the same event handlers it had before or it will have one additional event handler. Beware of "optimizations" that change behavior significantly.

> > **VLADIMIR RESHETNIKOV** The Microsoft C# compiler does not cache delegate instances within generic methods.

## 6.5.2 Evaluation of Anonymous Function Conversions to Expression Tree Types

Conversion of an anonymous function to an expression tree type produces an expression tree (§4.6). More precisely, evaluation of the anonymous function conversion leads to the construction of an object structure that represents the structure of the anonymous function itself. The precise structure of the expression tree, as well as the exact process for creating it, are implementation defined.

> > **VLADIMIR RESHETNIKOV** Like a delegate, an expression tree can have a set of captured outer variables.

## 6.5.3 Implementation Example

This section describes a possible implementation of anonymous function conversions in terms of other C# constructs. The implementation described here is based on the same principles used by the Microsoft C# compiler, but it is by no means a mandated implementation, nor is it the only one possible. It only briefly mentions conversions to expression trees, as their exact semantics are outside the scope of this specification.

The remainder of this section gives several examples of code that contains anonymous functions with different characteristics. For each example, a corresponding translation to code that uses only other C# constructs is provided. In the examples, the identifier D is assumed to represent the following delegate type:

```
public delegate void D();
```

The simplest form of an anonymous function is one that captures no outer variables:

```
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

This can be translated to a delegate instantiation that references a compiler-generated static method in which the code of the anonymous function is placed:

```
class Test
{
    static void F() {
        D d = new D(__Method1);
    }
    static void __Method1() {
        Console.WriteLine("test");
    }
}
```

In the following example, the anonymous function references instance members of this:

```
class Test
{
    int x;
    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

This can be translated to a compiler-generated instance method containing the code of the anonymous function:

```
class Test
{
    int x;
    void F() {
        D d = new D(__Method1);
    }
    void __Method1() {
        Console.WriteLine(x);
    }
}
```

In this example, the anonymous function captures a local variable:

```csharp
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

The lifetime of the local variable must now be extended to at least the lifetime of the anonymous function delegate. This can be achieved by “hoisting” the local variable into a field of a compiler-generated class. Instantiation of the local variable (§7.15.5.2) then corresponds to creating an instance of the compiler generated class, and accessing the local variable corresponds to accessing a field in the instance of the compiler-generated class. Furthermore, the anonymous function becomes an instance method of the compiler-generated class:

```csharp
class Test
{
    void F() {
        __locals1 __locals1 = new __locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;
        public void __Method1() {
            Console.WriteLine(y);
        }
    }
}
```

Finally, the following anonymous function captures this as well as two local variables with different lifetimes:

```csharp
class Test
{
    int x;
    void F() {
        int y = 123;
        for (int i = 0; i < 10; i++) {
            int z = i * 2;
            D d = () => { Console.WriteLine(x + y + z); };
        }
    }
}
```

Here, a compiler-generated class is created for each statement block in which locals are captured, such that the locals in the different blocks can have independent lifetimes. An instance of `__locals2`, the compiler-generated class for the inner statement block, contains the local variable z and a field that references an instance of `__locals1`. An instance of `__locals1`, the compiler-generated class for the outer statement block, contains the local variable y and a field that references `this` of the enclosing function member. With these data structures, it is possible to reach all captured outer variables through an instance of `__locals2`, and the code of the anonymous function can thus be implemented as an instance method of that class.

> > **BILL WAGNER** If `F()` returned an instance of `D`, the lives of all the variables this function captures would be extended.

```
    class Test
    {
        void F() {
            __locals1 __locals1 = new __locals1();
            __locals1.__this = this;
            __locals1.y = 123;
            for (int i = 0; i < 10; i++) {
                __locals2 __locals2 = new __locals2();
                __locals2.__locals1 = __locals1;
                __locals2.z = i * 2;
                D d = new D(__locals2.__Method1);
            }
        }

        class __locals1
        {
            public Test __this;
            public int y;
        }

        class __locals2
        {
            public __locals1 __locals1;
            public int z;

            public void __Method1() {
                Console.WriteLine(__locals1.__this.x + __locals1.y + z);
            }
        }
    }
```

The same technique applied here to capture local variables can also be used when converting anonymous functions to expression trees: References to the compiler-generated objects can be stored in the expression tree, and access to the local variables can be represented as field accesses on these objects. The advantage of this approach is that it allows the “lifted” local variables to be shared between delegates and expression trees.
