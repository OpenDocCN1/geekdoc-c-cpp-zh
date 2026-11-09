
在第四次作业中，你会发现使用 C# 的隐式类型局部变量特性的一些实际价值。如果没有这个特性，你必须在赋值运算符两边都指定 `Dictionary<String, Single>`。这不仅输入量大，而且如果你决定更改集合类型或任何泛型参数类型，那么你也不得不修改赋值运算符两边的代码。

在 `foreach` 循环中，我也使用 `var` 让编译器自动推断集合中元素的类型。这证明了在 `foreach`、`using` 和 `for` 语句中使用 `var` 是可行的，而且非常有用。在试验代码时它也很有用。例如，你用某个方法的返回类型初始化一个隐式类型局部变量，随着开发方法的进行，你可能会决定改变其返回类型。如果这样做，编译器会自动发现返回类型已改变，并自动更改变量的类型！这很妙，但当然，如果方法中的其他代码使用该变量并假定它是旧类型来访问成员，那么这些代码可能无法再编译。

在 Microsoft Visual Studio 中，你可以将鼠标光标悬停在源代码中的 `var` 上，编辑器会显示一个工具提示，告诉你编译器从表达式推断出的类型。在方法内使用匿名类型时，必须使用 C# 的隐式类型局部变量特性；更多细节请参见第 10 章“属性”。

你不能使用 `var` 声明方法的参数类型。原因你应该很清楚：编译器必须从调用点的参数推断参数的类型，而可能没有调用点，也可能有很多调用点。此外，你不能使用 `var` 声明类型的字段。C# 有此限制的原因有很多。原因之一是字段可以被多个方法访问，C# 团队认为这个契约（变量的类型）应该明确声明。另一个原因是，如果允许这样做，将使匿名类型（在第 10 章讨论）泄漏到单个方法之外。

> **重要提示** 不要混淆 **dynamic** 和 **var**。使用 **var** 声明局部变量只是一种语法快捷方式，让编译器从表达式推断出具体数据类型。**var** 关键字只能用于在方法内声明局部变量，而 **dynamic** 关键字可用于局部变量、字段和参数。你不能将表达式强制转换为 **var**，但可以将表达式强制转换为 **dynamic**。使用 **var** 声明的变量必须显式初始化，而使用 **dynamic** 声明的变量则不必初始化。有关 C# 的 **dynamic** 类型的更多信息，请参见第 5 章“dynamic 原始类型”一节。

**v** 所指向的 **Int32** 被更改为 **10**。当 **GetVal1** 返回时，**Main** 的 **x** 的值为 **10**，控制台上显示 10。对大型值类型使用 **out** 是高效的，因为这样可以防止在方法调用时复制值类型字段的实例。

现在让我们来看一个使用 **ref** 而不是 **out** 的示例：

```csharp
public sealed class Program {
    public static void Main() {
        Int32 x = 5;        // x is initialized
        AddVal(ref x);      // x must be initialized.
        Console.WriteLine(x); // Displays "15"
    }

    private static void AddVal(ref Int32 v) {
        v += 10; // This method can use the initialized value in v.
    }
}
```

在这段代码中，**x** 也在 **Main** 的栈帧中声明，并被初始化为 **5**。然后 **x** 的地址被传给 **AddVal**。**AddVal** 的 **v** 是指向 **Main** 栈帧中 **Int32** 值的指针。在 **AddVal** 内部，**v** 指向的 **Int32** 必须已有一个值。因此，**AddVal** 可以在它想要的任何表达式中使用初始值。**AddVal** 也可以更改该值，新值将被“返回”给调用者。在此示例中，**AddVal** 将 **10** 加到初始值上。当 **AddVal** 返回时，**Main** 的 **x** 将包含 **15**，这就是控制台上显示的内容。

总而言之，从 IL 或 CLR 的角度来看，**out** 和 **ref** 做的事情完全一样：它们都导致传递指向实例的指针。区别在于编译器会帮助确保你的代码正确。下面这段试图将未初始化的值传给期望 **ref** 参数的方法的代码，会产生以下消息："error CS0165: Use of unassigned local variable 'x'."

```csharp
public sealed class Program {
    public static void Main() {
        Int32 x;            // x is not initialized.

        // The following line fails to compile, producing
        // error CS0165: Use of unassigned local variable 'x'.
        AddVal(ref x);

        Console.WriteLine(x);
    }

    private static void AddVal(ref Int32 v) {
        v += 10; // This method can use the initialized value in v.
    }
}
```

![](img/3c46ff5b170881db4209d365b1f7a808_244_0.png)

**重要提示** 经常有人问我，为什么 C# 要求调用方法时必须指定 **out** 或 **ref**。毕竟，编译器知道被调用的方法是否需要 **out** 或 **ref**，应该能够正确编译代码。事实证明，编译器确实可以自动做出正确的处理。然而，C# 语言的设计者认为调用者应该明确表达其意图。这样在调用点，被调用的方法预期会改变所传递变量的值，这一点就显而易见了。

此外，CLR 允许你根据 **out** 和 **ref** 参数的使用方式重载方法。例如，在 C# 中，以下代码是合法的，并且可以正常编译：

```csharp
public sealed class Point {
    static void Add(Point p) { ... }
    static void Add(ref Point p) { ... }
}
```

仅因 **out** 和 **ref** 不同而重载方法是不合法的，因为这些方法的签名在元数据表示中是相同的。因此，我不能在前面的 **Point** 类型中再定义以下方法：

```csharp
static void Add(out Point p) { ... }
```

如果你试图将最后一个 **Add** 方法包含在 **Point** 类型中，C# 编译器会发出以下消息：**error CS0663: 'Add' cannot define overloaded methods that differ only on ref and out.**

将 **out** 和 **ref** 与值类型一起使用，会得到与按值传递引用类型时相同的行为。对于值类型，**out** 和 **ref** 允许方法操作单个值类型实例。调用者必须为实例分配内存，被调用者操作该内存。对于引用类型，调用者为指向引用对象的指针分配内存，被调用者操作该指针。由于这种行为，将 **out** 和 **ref** 与引用类型一起使用，仅当方法要“返回”一个它所知道的对象的引用时才有用。以下代码演示：

```csharp
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs;   // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        // Continue while there are more files to process.
        for (; fs != null; ContinueProcessingFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }
}
```

## 向方法传递可变数量的参数

有时，开发者定义一个可以接受可变数量参数的方法会很方便。例如，**System.String** 类型提供了一些方法，允许将任意数量的字符串连接在一起，还提供了一些方法，允许调用者指定一组要一起格式化的字符串。

要声明一个接受可变数量参数的方法，你可以按如下方式声明该方法：

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

除了应用于方法签名最后一个参数的 **params** 关键字之外，这个方法中的一切对你来说应该都非常熟悉。暂时忽略 **params** 关键字，很明显，这个方法接受一个 **Int32** 值数组，并遍历该数组，将所有值加起来。得到的 **sum** 返回给调用者。

显然，代码可以像下面这样调用这个方法：

```csharp
public static void Main() {
    // Displays "15"
    Console.WriteLine(Add(new Int32[] { 1, 2, 3, 4, 5 }));
}
```

很明显，数组可以很容易地用任意数量的元素初始化，然后传给 **Add** 进行处理。尽管前面的代码能够编译并正确运行，但有点难看。作为开发者，我们当然更愿意按如下方式编写对 **Add** 的调用：

```csharp
public static void Main() {
    // Displays "15"
    Console.WriteLine(Add(1, 2, 3, 4, 5));
}
```

你会很高兴地知道，因为有了 **params** 关键字，我们可以做到这一点。**params** 关键字告诉编译器将 **System.ParamArrayAttribute** 自定义特性的一个实例应用到该参数上。
