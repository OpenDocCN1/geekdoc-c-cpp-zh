
向各种工具和实用程序指明，此方法是由编译器而非程序员生成的。然后，=> 运算符右侧的代码会被放入这个编译器生成的方法中。

> **注意** 编写 lambda 表达式时，无法将自己的自定义特性应用到编译器生成的方法上。此外，也不能向该方法应用任何方法修饰符（例如 `unsafe`）。不过这通常不是问题，因为编译器生成的匿名方法最终总是私有的，并且方法是静态还是非静态取决于它是否访问任何实例成员。因此，没有必要向该方法应用诸如 `public`、`protected`、`internal`、`virtual`、`sealed`、`override` 或 `abstract` 之类的修饰符。

最后，如果你编写上面所示的代码并进行编译，就仿佛 C# 编译器将你的代码重写成了这样（注释是我添加的）：

```csharp
internal sealed class AClass {
    // This private field is created to cache the delegate object.
    // Pro: CallbackWithoutNewingADelegateObject will not create
    //     a new object each time it is called.
    // Con: The cached object never gets garbage collected
    [CompilerGenerated]
    private static WaitCallback <>9__CachedAnonymousMethodDelegate1;

    public static void CallbackWithoutNewingADelegateObject() {
        if (<>9__CachedAnonymousMethodDelegate1 == null) {
            // First time called, create the delegate object and cache it.
            <>9__CachedAnonymousMethodDelegate1 =
                new WaitCallback(<CallbackWithoutNewingADelegateObject>b__0);
        }
        ThreadPool.QueueUserWorkItem(<>9__CachedAnonymousMethodDelegate1, 5);
    }

    [CompilerGenerated]
    private static void <CallbackWithoutNewingADelegateObject>b__0(Object obj) {
        Console.WriteLine(obj);
    }
}
```

lambda 表达式必须与 WaitCallback 委托的签名匹配：它返回 void，并且接受一个 Object 参数。不过，我只是通过将 obj 放在 => 运算符的左侧来指定参数名称。在 => 运算符的右侧，Console.WriteLine 恰好返回 void。然而，如果我放置的表达式不返回 void，编译器生成的代码会直接忽略该返回值，因为编译器生成的方法必须具有 void 返回类型才能满足 WaitCallback 委托。

同样值得注意的是，匿名函数被标记为 private；这会禁止任何未在类型内部定义的代码访问该方法（尽管反射会揭示该方法确实存在）。另外，请注意匿名方法被标记为 static；这是因为代码没有访问任何实例成员（它也不能访问，因为 CallbackWithoutNewingADelegateObject 本身是一个静态方法）。但是，代码可以引用类中定义的任何静态字段或静态方法。示例如下：

```csharp
internal sealed class AClass {
    private static String sm_name;    // A static field

    public static void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(
            // The callback code can reference static members.
            obj => Console.WriteLine(sm_name + ": " + obj),
            5);
    }
}
```

如果 CallbackWithoutNewingADelegateObject 方法不是静态的，那么匿名方法的代码就可以包含对实例成员的引用。如果它不包含对实例成员的引用，编译器仍会生成一个静态匿名方法，因为这比实例方法更高效，且不需要额外的 this 参数。但是，如果匿名方法的代码确实引用了实例成员，编译器将生成一个非静态匿名方法：

```csharp
internal sealed class AClass {
    private String m_name;    // An instance field

    // An instance method
    public void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(
            // The callback code can reference instance members.
            obj => Console.WriteLine(m_name + ": " + obj),
            5);
    }
}
```

=> 运算符的左侧是你指定要传递给 lambda 表达式的任何参数名称的位置。你必须遵循一些规则。请看下面的示例：

```csharp
// If the delegate takes no arguments, use ()
Func<String> f = () => "Jeff";

// If the delegate takes 1+ arguments, you can explicitly specify the types
Func<Int32, String> f2 = (Int32 n) => n.ToString();
Func<Int32, Int32, String> f3 = (Int32 n1, Int32 n2) => (n1 + n2).ToString();

// If the delegate takes 1+ arguments, the compiler can infer the types
Func<Int32, String> f4 = (n) => n.ToString();
Func<Int32, Int32, String> f5 = (n1, n2) => (n1 + n2).ToString();

// If the delegate takes 1 argument, you can omit the ()s
Func<Int32, String> f6 = n => n.ToString();

// If the delegate has ref/out arguments, you must explicitly specify ref/out and the type
Bar b = (out Int32 n) => n = 5;
```

对于最后一个示例，假设 Bar 定义如下：

```csharp
delegate void Bar(out Int32 z);
```

=> 运算符的右侧是你指定匿名函数体的位置。函数体通常由一个简单或复杂的表达式组成，该表达式最终返回一个非 void 的值。在上面的代码中，我将返回 String 的 lambda 表达式赋值给了所有 Func 委托变量。函数体由单个语句组成的情况也很常见。例如，当我调用 ThreadPool.QueueUserWorkItem 时，向它传递了一个调用 Console.WriteLine（返回 void）的 lambda 表达式。

如果你希望函数体由两个或更多语句组成，则必须用大括号将它括起来。如果委托期望一个返回值，那么你必须在函数体内包含一条 return 语句。示例如下：

```csharp
Func<Int32, Int32, String> f7 = (n1, n2) => { Int32 sum = n1 + n2; return sum.ToString(); };
```

**重要** 如果这一点尚不明显，请允许我明确指出，lambda 表达式的主要好处是它们消除了源代码中的一层间接性。通常，你必须编写一个单独的方法，为该方法命名，然后在需要委托的地方传递该方法的名称。名称为你提供了一种引用代码体的方式，如果你需要在源代码中的多个位置引用相同的代码体，那么编写一个方法并为其命名是一种很好的做法。然而，如果你需要让一个代码体仅在源代码中被引用一次，那么 lambda 表达式允许你直接内联放置该代码，而无需为其命名，从而提高了程序员的工作效率。

**注意** 当 C# 2.0 发布时，它引入了一个名为*匿名方法*的特性。与 lambda 表达式（在 C# 3.0 中引入）一样，匿名方法描述了一种创建匿名函数的语法。现在（见 C# 语言规范第 7.14 节）建议开发人员使用更新的 lambda 表达式语法，而不是较旧的匿名方法语法，因为 lambda 表达式语法更简洁，使代码更易于编写、阅读和维护。当然，微软的 C# 编译器继续支持解析这两种创建匿名函数的语法，因此开发人员不必修改任何最初为 C# 2.0 编写的代码。在本书中，我将只解释和使用 lambda 表达式语法。

## 语法快捷方式 #3：无需手动将局部变量包装到类中即可将其传递给回调方法

我已经展示了回调代码如何引用类中定义的其他成员。然而，有时你可能希望回调代码引用定义方法中存在的局部参数或变量。下面是一个有趣的示例：

```csharp
internal sealed class AClass {
   public static void UsingLocalVariablesInTheCallbackCode(Int32 numToDo) {
      // Some local variables
```
