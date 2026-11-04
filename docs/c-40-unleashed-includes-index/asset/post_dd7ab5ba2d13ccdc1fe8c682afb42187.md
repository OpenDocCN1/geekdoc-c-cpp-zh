
The compilation for the remaining leaf node is equally simple because it simply loads an integer constant value. The `ldc.i4` instruction is used for this, as shown here:

```csharp
class Const : Expression
{
    public int Value { get; set; }

    public override void Compile(ILGenerator gen, Dictionary<Param, int> env)
    {
        gen.Emit(OpCodes.Ldc_I4, Value);
    }
}
```

Finally, we take a look at the most complicated expression, the Arithmetic one. Here, we need to visit the child subtrees first, in a left-to-right order, so that the code that's responsible for calculating the subexpressions gets evaluated first. Once those two calls have been made, we can emit the IL instruction corresponding to the arithmetic operation, which will, at runtime, pop the two values on the top of the stack and combine them using the arithmetic operation:

```csharp
class Arithmetic : Expression
{
    public Expression Left { get; set; }
    public Expression Right { get; set; }
    public Operation Operation { get; set; }

    public override void Compile(ILGenerator gen, Dictionary<Param, int> env)
    {
        Left.Compile(gen, env);
        Right.Compile(gen, env);
        switch (Operation)
        {
            case Operation.Add:
                gen.Emit(OpCodes.Add);
                break;
            case Operation.Multiply:
                gen.Emit(OpCodes.Mul);
                break;
            case Operation.Subtract:
                gen.Emit(OpCodes.Sub);
                break;
            case Operation.Divide:
                gen.Emit(OpCodes.Div);
                break;
        }
    }
}
```

Now that we have all the intermediate nodes, we still need to write the entry point to this whole translation. Because the top-level construct is the Function, we provide a specialized Compile method on it with the following signature:

```csharp
public T Compile<T>()
```

Here T is a delegate type that will be used for the result of the compilation so that the caller can make a statically typed call to the compiled function. For example, our example expression f could be compiled and executed as follows, using one of the built-in generic delegate types:

```csharp
var res = f.Compile<Func<int, int, int>>();
Console.WriteLine(res(2, 3)); // 10 = (2 + 3) * 2
```

The top-level Compile method is relatively straightforward and contains all the plumbing to create a dynamic assembly, as we've seen before. Additional code takes care of establishing the environment data structure, based on the number of parameters specified on the Function instance:

```csharp
public T Compile<T>()
{
    var asm = AppDomain.CurrentDomain.DefineDynamicAssembly(
        new AssemblyName("LCG"),
        AssemblyBuilderAccess.RunAndCollect);

    var mod = asm.DefineDynamicModule("Lightweight");
    var tpe = mod.DefineType("Code");
    var mtd = tpe.DefineMethod("Generation",
        MethodAttributes.Public | MethodAttributes.Static,
        // Return type
        typeof(int),
        // Every of the Parameters.Count parameters is of type int as well
        Enumerable.Repeat(typeof(int), this.Parameters.Count).ToArray()
    );

    // Establish environment; we could also use a List<T> and use IndexOf
    // in the recursive compilation code to find the parameter's index.
    var env = new Dictionary<Param, int>();
    int arg = 0;
    foreach (var par in Parameters)
        env[par] = arg++;

    // Compilation is requested for the Body, and a final "ret" instruction
    // is added to the IL generator.
    var gen = mtd.GetILGenerator();
    this.Body.Compile(gen, env);
    gen.Emit(OpCodes.Ret);

    var res = tpe.CreateType();

    // Create a delegate of the specified type, referring to the generated
    // method which we always call "Generation" (see the DefineMethod call).
    return (T)(object)Delegate.CreateDelegate(typeof(T),
        res.GetMethod("Generation"));
}
```

Because the recursive nature of the compilation may be a bit abstract to grasp at first, some visualization can help. Figure 21.15 shows the compilation for our sample expression tree. The final step where the Compile call on Body returns is omitted from the diagram but simply appends the final return instruction to the output. It's worth tracing through the compilation code under the debugger to see this tree traversal in action, too.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1119_0.png)

FIGURE 21.15 Compilation of our expression tree, using a depth-first traversal.

## WHY BOTHER?

As mentioned before, most readers will likely never have to deal with LCG directly. However, the whole discussion earlier about the feature serves as a great basis for the understanding of expression trees, which are discussed next. In fact, the compilation feature for the built-in expression trees is based on the same technology and follows a similar tree-traversal mechanism to drive compilation into IL code.

## Saving the Assembly to Disk

One final remark about LCG is that it can save the compiled assembly to disk, instead of just using it for immediate execution. This can be useful if you're writing some kind of compiler that needs to persist its results to disk:

```csharp
var asm = AppDomain.CurrentDomain.DefineDynamicAssembly(
    new AssemblyName("LCG"), AssemblyBuilderAccess.RunAndSave);
...
asm.Save(fileName);
```

You are invited to try this out on our expression tree compiler. After the assembly has been saved to disk, add it as a reference to a Visual Studio project and call the generated method (whose name you likely want to change in the Compile method).

## Expression Trees

In the C# 3.0 era, coinciding with the .NET Framework 3.5 release, the mission to solve the impedance mismatch between object-oriented programming and various data models required the ability to represent code as data. In Chapter20, “Language Integrated Query Internals,” you saw how LINQ query expressions translate into chains of query operator method calls. For query providers to be able to make sense of the querying intent specified by the user, all information captured in the invocations of query operators needs to be available in an object model at runtime. To solve this problem, expression trees were introduced.

We now take a look at two sides spanned by expression trees. One is the generation of expression trees by the compiler, as leveraged in the translation of query expressions that target the IQueryable<T> interface (see Chapter20). The other is the runtime aspect of expression trees, in particular the object model and auxiliary APIs that allow you to visit the expression tree or to compile it into IL code. Finally, we also detail the evolution of those expression trees into statement trees in .NET 4, which allows them to be used as the core infrastructure for the DLR.

### Compiler-Generated Expression Trees

As mentioned in Chapter 20, lambda expressions have two representations. One is the equivalent to anonymous methods, causing the lambda expression to be translated into a piece of IL code that allows direct execution of its logic:

```csharp
Func<int, int, int> f = (a, b) => (a + b) * 2;
```

This is the same as the following C# 2.0 fragment:

```csharp
Func<int, int, int> f = delegate (int a, int b) { return (a + b) * 2; };
```

The preceding can be translated into a separate method that's being referred to by the delegate:

```csharp
Func<int, int, int> f = new Func<int, int, int>(MyExpression);
...
static int MyExpression(int a, int b) { return (a + b) * 2; }
```

However, when we assign the lambda expression to an Expression<T>, where T is a delegate type, the compiler's code generation path deviates and emits IL code that will construct an expression tree representing the lambda expression at runtime. Expression tree APIs are defined in the System.Linq.Expressions namespace, revealing their first use and introduction in .NET 3.5:

```csharp
Expression<Func<int, int, int>> f = (a, b) => (a + b) * 2;
```

Using .NET Reflector, it's easy to see the code that gets generated for the line of preceding code (assuming their decompiler doesn't become smarter in future versions):

```csharp
ParameterExpression a, b;
Expression<Func<int, int, int>> expression =
    Expression.Lambda<Func<int, int, int>>(
        Expression.Multiply(
            Expression.Add(
                a = Expression.Parameter(typeof(int), "a"),
                b = Expression.Parameter(typeof(int), "b")),
            Expression.Constant(2, typeof(int))),
        new [] { a, b });
}
```

Expression trees are generated whenever a lambda expression gets assigned to any kind of variable (which can be a local, a parameter, or a field) that's typed as Expression<T>. Notice the use of the word *expression*. In particular, lambdas with statement bodies cannot be turned into expression trees (because they require statement trees), as shown in figure 21.16.
