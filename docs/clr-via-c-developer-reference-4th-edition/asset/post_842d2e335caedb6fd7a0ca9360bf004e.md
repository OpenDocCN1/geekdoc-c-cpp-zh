
When you build and run this code, the following output appears.

The light is off

Failed to get status from Fan.Speed
Error: The fan broke due to overheating

The volume is loud

## Enough with the Delegate Definitions Already
(Generic Delegates)

Many years ago, when the .NET Framework was just starting to be developed, Microsoft introduced the notion of delegates. As programmers were adding classes to the FCL, they would define new delegate types that they introduced a callback method. Over time, many, many delegates got defined. In fact, in CoreLib.dll alone, 50 delegate types are now defined. Let's just look at a few of them.

```c
public delegate void TryCode(Object userData);
public delegate void WaitCallback(Object state);
public delegate void TimerCallback(Object state);
public delegate void ContextCallback(Object state);
public delegate void SendPostCallback(Object state);
public delegate void ParameterizedThreadStart(Object obj);
```

Do you notice anything similar about the delegate definitions that I selected? They are really all the same: a variable of any of these delegate types must refer to a method that takes an Object and returns void. There is really no reason to have all of these types defined; really that needs to be one.

In fact, that .NET Framework supports generics, we really just need a few generics (in the System namespace) that represent methods that take up to 16 arguments.

```csharp
public delegate void Action(); // OK, this one is not generic
public delegate void Action<T>(T obj);
public delegate void Action<T1, T2>(T1 arg1, T2 arg2);
public delegate void Action<T1, T2, T3>(T1 arg1, T2 arg2, T3 arg3);
public delegate void Action<T1, ..., T16>(T1 arg1, ..., T16 arg16);
```

So the .NET Framework now ships with 17 Action delegates that range from having no arguments to 16 arguments. If you ever need to call a method that has more than 16 arguments, you will be forced to define your own delegate type, but this is very unlikely.

In addition to the Action delegates, the .NET Framework ships with 17 Func delegates, which allow the callback method to return a value.

```csharp
public delegate TResult Func<T>();
public delegate TResult Func<T, TResult>(T arg);
public delegate TResult Func<T1, T2, TResult>(T1 arg1, T2 arg2);
public delegate TResult Func<T1, T2, T3, TResult>(T1 arg1, T2 arg2, T3 arg3);
```

```csharp
public delegate TResult Func<T1, ..., T16, TResult>(T1 arg1, ..., T16 arg6);
```

It is recommended that these delegates be used wherever possible instead of defining even more delegates in their code. This reduces the number of types in the system and also simplifies coding. However, you might have to define your own delegate if you need to pass an argument by reference using the ref or out keyword.

```csharp
delegate void Bar(ref int i32);
```

You may also have to do this if you want your delegate to take a variable number of arguments via C#'s keyword, if you need to specify any values for any of your delegate's arguments, or if you need to constrain a delegate's generic type.

When using delegates that take generic arguments and return values, contra-variance and covariance come into play, and it is recommended that you take advantage of these features because they have no ill effects and allow your delegates to be used in more scenarios. For more information about this, see the "Delegate and Interface Contra-variant and Covariant Generic Type Arguments" section in Chapter 12, "Generics."

## C#'s Syntactic Sugar for Delegates

Most programmers find working with delegates to be cumbersome because the syntax is so strange. For example this line of code:

```csharp
button1_Click += new EventHandler(button1_Click);
```

where button1_Click is a method that looks something like this:

```csharp
void button1_Click(object sender, EventArgs e) {
  // Do something, the button was clicked...
}
```

The idea behind the first line of code is to register the address of the button1_Click method with a button control so when the button is clicked, the method will be called. To most programmers, it feels unnatural to construct an EventHandler delegate object just to specify the address of the button1Click method. However, constructing the EventHandler delegate object is required for the CLR this object provides a wrapper that ensures the method can be called only in a type-safe fashion. The wrapper also allows the calling of instance methods and chaining. Unfortunately, most programmers don't want to think about these details. Programmers prefer to write the preceding code as follows.

```csharp
button1.Click += button1Click;
```

Fortunately, Microsoft's C# compiler offers programmers some syntax shortcuts when working with delegates. I'll explain all of these shortcuts in this section. Last one point before we begin: I'm about to describe really boils down to C# syntactic sugar; these new syntax shortcuts are really just giving programmers an easier way to produce the IL that is generated so that the CLR and other programming languages can work with delegates. This also means that I'm about to describe specific to C#; other compilers might not offer the additional delegate syntax shortcuts.

## Syntactical Shortcut #1: No Need to Construct a Delegate Object

As demonstrated already, C# allows you to specify the name of a callback method without having to construct a delegate object wrapper. Here is another example:

```csharp
internal sealed class {
    public static void CallbackNewingObject() {
        ThreadPool.QueueUserItem();
    }

    private static void AsyncTask(Object o) {
        Console.WriteLine(o);
    }
}
```

The compiler chooses to start method name with a < sign as in C#, an identifier cannot contain a < sign; this ensures that you will not accidentally define a method that coincides with the name the compiler has chosen. Incidentally, while C# forbids identifiers to contain a < sign, the CLR allows it. Also, note that although you could access the method via reflection by passing the method name as a string, the C# language specifies that there is no guarantee of how the compiler generates the name. For example, each time you compile the code, the compiler could produce a different name for the method.

## Syntactical Shortcut #2: No Need to Define a Method (Lambda Expressions)

In the preceding code, the C# allows you to write inline so it doesn't have its own. For example, the preceding code could be rewritten as:

```csharp
internal sealed class {
    public static void CallbackNewingObject(obj => Console.WriteLine(obj));
}
```

Notice that the first "argument" is to the QueueUserItem method. More formally, the italicized code is a C# lambda expression: =>. You may use a lambda expression in your code where the compiler would normally expect a delegate. And when the compiler sees the use of this lambda expression, the compiler automatically defines a new method in the class this new method is called an anonymous function because the compiler creates the name automatically, and normally you wouldn't know its name.

Using ILasm, you might notice that the C# compiler applies the System.Runtime.CompilerGeneratedAttribute attribute to this method to indicate to tools and utilities that this was produced by a compiler as opposed to a programmer. The code to the right of the => operator is then placed in this compiler-generated method.

> When writing a lambda expression, there is no way to apply your custom attribute to the compiler-generated method. Furthermore, you cannot apply any modifiers (such as unsafe) to the method. This is usually not a problem because anonymous methods generated by the compiler always end up private, and the method is either static or static depending on whether the method accesses any instance members. So there is no need to apply modifiers as public, protected, internal, virtual, sealed, override, or abstract to the method.
