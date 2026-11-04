
be slightly disappointed to see there's nothing of interest in there apart from a subtle hint that the implementation of those methods is provided by the runtime. Figure 17.5 shows the Invoke method definition from an ILDASM point of view.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_814_0.png)

FIGURE 17.5 Low-level plumbing is the common language runtime's business.

## AN ALTERNATIVE VIEW

If the concept of delegate types is a bit confusing at first, think of them slightly differently. Delegates are similar to interfaces with a single method inside them, corresponding to the Invoke method we've seen in ILDASM. In fact, platforms such as Java that have historically omitted delegates from the language specification realize similar capabilities by means of one-method interfaces such as Runnable. With this analogy in mind, creating a delegate instance is similar to implementing that single method on the interface.

Delegate type declarations are similar to method declarations in their expressive power. You can use ref and out parameters and params arrays, as shown here:

```
delegate string Foo(int a, ref double b, out long c, params DateTime[] ds);
```

The parameter list of a delegate type can be empty, and the return type of a delegate can be void. Examples of such delegates can be found in the System.Threading namespace and the System namespace:

```
delegate void ThreadStart(); // for Java folks: similar to Runnable.run
delegate void Action();
```

## NOMINAL EQUIVALENCE

Delegate types in C# have so-called nominal equivalence, in contrast to so-called structural equivalence. This means that two delegate types with the same parameter list and return type are considered different. In the preceding example, Action and ThreadStart can refer to the same methods but are considered different types.

Delegate types can also be declared using generics, examples of which can be found in the System namespace in the form of the Func and Action delegate types:

```
delegate TResult Func<out TResult>();
delegate TResult Func<in T1, out TResult>(T1 t1);
...
delegate TResult Func<in T1, ..., in T16, out TResult>(T1 t1, ..., T16 t16);

delegate void Action();
delegate void Action<in T1>(T1 t1);
...
delegate void Action<in T1, ..., in T16>(T1 t1, ..., T16 t16);
```

For example, to represent a function that takes an integer value and produces a bool, you could use the unary (that is, with one argument) generic Func delegate type; and to create an integral sum function, the binary generic Func delegate type can be used:

```
Func<int, bool> isEven = new Func<int, bool>(IsEven);
Func<int, int, int> add = new Func<int, int, int>(Add);
```

## GENERIC CO- AND CONTRAVARIANCE

Notice the use of the in and out modifiers on the generic parameters on the Func and Action delegate types. During our discussion about generics, you learned about this C# 4.0 feature called generic co- and contravariance. This feature enables the following scenario that failed to compile before in C# 3.0:

```
Func<Fruit, string> printFruit = new Func<Fruit, string>(FruitPrinter);
Func<Apple, object> appleToObject = printFruit; // failed in C# 3.0
```

Before generic co- and contravariance, C# 2.0 already provided the notion of co- and contravariance for creating a delegate from a method group that doesn’t have a signature that matches exactly with the target delegate’s signature:

```
// Assume the following definition:  string PrintFruit(Fruit f);
Func<Apple, object> appleToObject = PrintFruit;
```

The compiler can prove this is safe to do because of the subtype relationships that exist between Apple and Fruit and string and object. If we pass an Apple to appleToObject, it’s fine for the PrintFruit target to treat it as a Fruit. For the return type, it’s safe to treat the string that came back from PrintFruit as an object.

Method group conversion refers to the capability of the compiler to figure out from context what method from the group is meant, based on the delegate type the method group gets assigned to. For more information, refer to the C# language specification, where all rules for method group conversion are outlined.

The two previous code fragments are completely identical from an intermediate language (IL) point of view, so it's time to take a look at how delegate instantiation works behind the scenes. Figure 17.7 illustrates this.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_817_0.png)

FIGURE 17.7 Delegate instantiation from an IL perspective.

You've already seen the constructor function on the delegate type in the previous section, so no surprises there. It takes two arguments, one of which denotes the object instance on which to invoke the target method. Because we're using a static method in our example, there's no instance, and hence the ldnull instruction is emitted. The way to refer to a method is observed on the line following the ldnull instruction, using ldftn, which results in a native int. It's this native int value that points at the method and allows the CLR to call into the method when requested to do so by means of delegate invocation. Notice that I didn't lie about how the delegate is getting called. Line IL_0011 clearly shows a call to Invoke being emitted for the delegate invocation.

Based on the discussion here you will have guessed delegate instances can refer to instance methods as well:

```
static void Main() {
    var calc = new Calculator(); // with an Add instance method
    BinOp add = calc.Add;
    int three = add(1, 2); // calls the Add method on calc through the delegate
}
```

## EASIER THAN C-STYLE FUNCTION POINTERS

The ability to use the exact same delegate type to refer to either a static method or an instance method is a blessing. Behind the scenes, the calls to the target methods are quite different for both cases, due to the need for a “this pointer” when making an instance method call. The CLR’s delegate system abstracts all those details away nicely, which is great compared to the world of C-style function pointers, where this often poses problems and frustration when calling conventions and such.

## Anonymous Function Expressions

That’s a good start, but the need to create a method even for the tiniest of methods to be used or passed as a delegate is quite cumbersome, too. Why do we need to create a whole Add method with the appropriate signature if we just want to express “add two numbers”? Can’t we just somehow declare the method “inline” and have the compiler take care of creating a method under the hood that’s referred to by the delegate? C# 2.0 introduced such a feature, called anonymous function expressions:

```
static void Main() {
    BinOp add = delegate (int a, int b) { return a + b; };
    int three = add(1, 2); // calls the anonymous method through the delegate
}
```

In the preceding code, we’re declaring an addition method inline by reusing the delegate keyword. Under the hood, the compiler generates an anonymous method containing the return a + b part and creates an instance of the BinOp delegate referring to the generated method. This plumbing, taken care of by the compiler, is shown in Figure 17.8.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_818_0.png)

FIGURE 17.8 Anonymous function expression generated target method.

The code generated in the Main method to refer to the generated method roughly looks like this:

```csharp
static void Main() {
    if (CS$<>9__CachedAnonymousMethodDelegate1 == null) {
        CS$<>9__CachedAnonymousMethodDelegate1 = new BinOp(<Main>b__0);
    }

    BinOp add = CS$<>9__CachedAnonymousMethodDelegate1;
    int three = add(1, 2); // calls the anonymous method through the delegate
}
```

Notice the little optimization by means of anonymous method delegate caching, so that subsequent calls of the containing method would not have to create a new instance of the delegate each time.

## KEEP DEBUGGABILITY IN MIND

> > Although tool support for anonymous function expressions is great with full-fidelity source code matching under the debugger (so you can just step through the inline method declaration), things get a bit more obscure when you’re faced with an exception call stack without a debugger nearby. Seeing a crash in a method like `<Main>b__0` might not be incredibly helpful at first sight. Luckily, the name of the containing method is still visible, but if you end up with huge inline method declarations, it might be time to introduce a dedicated method with a proper name.
> >
> > Personally, I tend to use anonymous function expressions (and lambda expressions) for short inline method declarations not exceeding a handful of statements, typically even just one single expression in case of lambdas.

## Closures: Captured Outer Variables

![](img/a16f85e62ce9bdc527f4b09dbfe26092_819_0.png)

Because of their capability to capture local variables from the outer scope, anonymous function expressions are much more powerful than would seem to be the case at first glance. Let’s take a look at an example:

```csharp
static void Main() {
    int factor = 2;
    BinOp addAndFactor = delegate (int a, int b) { return factor * (a + b); };
    int six = addAndFactor(1, 2);
}
```

In the preceding code fragment, the local variable factor is captured inside the embedded inline method declaration. This is a powerful capability that reduces plumbing significantly. Imagine how you would communicate the factor value to a delegate if you could-
