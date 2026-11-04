# WHERE DOES THE NAME LAMBDA COME FROM?

You might wonder where all of a sudden, out of nowhere, a Greek letter is used to name a new language feature. Lambda expressions are based on the concepts from lambda calculus, a theory on mathematical computation created by Alonzo Church in the 1920s. The first language to introduce a feature named after it was LISP (in 1958), even with a LAMBDA keyword in its language to denote something similar to C#'s lambda expressions nowadays.

This once more illustrates that all good ideas come from mathematics, although it takes a while for them to appear in widely used programming languages.

# Invoking Delegates

Creating delegate instances to refer to particular methods is a necessary step toward invoking those methods *through* the delegate. In passing, we've shown the way to do such invocations repeatedly: They just look like ordinary method calls. For example:

```
```csharp
Func<int, int, int> add = (a, b) => a + b;
int three = add(1, 2);
```
```

IntelliSense in Visual Studio will obviously give the caller a hand by showing what arguments are expected. Notice that names for those arguments come from the delegate type that's being used. In the preceding example, we're using one of the generic Func types, where arguments have names like arg1 and arg2. How this looks in Visual Studio is shown in Figure 17.10.

![](bbox=[0.057, 0.587, 0.362, 0.663])

FIGURE 17.10  Invoking a delegate feels like calling a method.

When a delegate passes arguments either by reference or as outputs, the use of those modifiers is required at the call site when specifying the arguments. This is completely similar to the way such methods are invoked directly, as well:

```
```csharp
// delegate string Foo(int a, ref double b, out long c, params DateTime[] ds);
Foo f = /* got it somehow */;
int a = 10;
double d = 12.34;
long c;
string res = f(a, ref d, out c, DateTime.Now);
```
```