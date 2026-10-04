
```cs
private static void ImplicitlyTypedLocalVariables() {
    var name = "Jeff";
    ShowVariableType(name); // Displays: System.String

    // var n = null; // Error: Cannot assign <null> to an implicitly-typed local variable
    var x = (String)null; // OK, but not much value
    ShowVariableType(x);

    var numbers = new Int32[] { 1, 2, 3, 4 };
    ShowVariableType(numbers); // Displays: System.Int32

    // Less typing for complex types
    var collection = new Dictionary<String, Single>() { { "Grant", 4.0f } };
    // Displays: System.Collections.Generic.Dictionary`2[System.String,System.Single]
    ShowVariableType(collection);

    foreach (var item in collection) {
        // Displays: System.Collections.Generic.KeyValuePair`2[System.String,System.Single]
        ShowVariableType(item);
    }
}

private static void ShowVariableType<T>(T t) {
    Console.WriteLine(typeof(T));
}
```

`ImplicitlyTypedLocalVariables` 方法内部的第一行代码通过 C# 的 `var` 标记引入了一个新变量。为了确定 `name` 的类型，编译器会查看赋值运算符 `=` 右侧的类型。`"Jeff"` 是一个字符串，编译器推断出 `name` 必须是 `String`。为了证明它正确推断了类型，我编写了 `ShowVariableType` 方法。这个泛型方法会推断其参数的类型，然后在控制台上显示它所推断的类型。为了方便阅读，我在 `ImplicitlyTypedLocalVariables` 方法内部添加了以注释形式展示的 `ShowVariableType` 输出结果。

`ImplicitlyTypedLocalVariables` 方法内部的第二次赋值（被注释掉）会产生编译器错误（错误 CS0815：无法将 <null> 赋值给隐式类型局部变量），因为 `null` 可以被隐式转换为任何类型或可空值值类型；编译器无法为 `null` 推断出具体的类型。然而，在第三次赋值中，我展示了如果你指定了类型（在我的示例中是 `String`），可以使用 `null` 初始化隐式类型的局部变量。尽管这是可行的，但如果你也可以写 `x = null;` 来获得结果，那么这样做就没有那么有用了。

在第四次赋值中，你看到了使用 C# 隐式类型局部变量功能处理的一些真实值。如果没有此功能，你必须在赋值运算符的两侧都指定 `Dictionary<String, Single>`。这不仅意味着大量的打字工作，而且如果你决定更改集合类型或任何泛型参数类型，你也必须修改赋值运算符两侧的代码。

在 `foreach` 循环中，我也使用 `var` 让编译器自动推断集合内部元素的类型。这证明了在 `foreach` 语句、`using` 语句和 `for` 语句中使用 `var` 是可行且非常有用的。它在实验代码时也可能很有用。例如，你根据方法的返回类型初始化隐式类型局部变量。如果你这样做，编译器会自动识别出返回类型已发生变化，并自动更改变量的类型！当然，如果方法中其他使用该变量的代码假设它是旧类型并访问其成员，那么代码可能将无法编译。

在 Visual Studio 中，你可以将鼠标光标悬停在源代码中的 `var` 上，编辑器将显示一个工具提示，显示编译器从表达式推断出的类型。在没有方法的情况下处理匿名类型时，必须使用 C# 的类型局部变量功能；更多细节请参见第 10 节“属性”。

你不能使用 `var` 声明方法的参数类型。这对你来说应该是显而易见的，因为编译器必须从调用时传递的参数推断参数类型，而可能没有调用处，或者有很多调用处。此外，你不能使用 `var` 声明字段。C# 有许多此限制的原因。其中一个原因是字段可以被多个方法访问，C# 团队认为合约（变量的类型）应该显式说明。另一个原因是这将允许匿名类型（在第 10 节讨论）从单个方法中泄露。

> **重要** 不要混淆 `var` 和 `dynamic`。通过 `var` 声明局部变量仅仅是一种语法快捷方式，编译器从表达式推断出特定的数据类型。`var` 关键字只能用于声明方法内部的局部变量，而 `dynamic` 关键字可以用于局部变量、字段和参数。你不能将表达式强制转换为 `var`，但可以强制转换为 `dynamic`。你必须显式初始化使用 `var` 声明的变量，而不需要初始化用 `dynamic` 声明的变量。有关关于 C# `dynamic` 类型的更多信息，请参见第 5 节中的“dynamic Primitive 类型”部分。

# 向方法引用引用参数

默认情况下，公共语言运行时（CLR）假设所有方法参数都是按值传递的。当传递引用类型对象时，对象的引用（或指针）被（按值）传递给方法。这意味着方法可以修改该对象，调用者将看到变化。对于值实例，实例的副本被传递给方法。这意味着方法获取了该值类型的私有副本，而调用者中的实例不受影响。

> **重要** 在方法中，你必须知道传递的每个参数是引用类型还是值类型，因为你编写用于操作参数的代码可能会显著不同。

CLR 允许你通过引用而非按值传递参数。在 C# 中，你可以通过 `out` 和 `ref` 关键字来实现这一点。关键字告诉 C# 编译器生成元数据，指示指定的参数是按引用传递的，编译器使用此代码传递参数的地址而不是参数本身。

从 CLR 的角度来看，`out` 和 `ref` 是相同的——也就是说，无论使用哪种关键字，生成的 IL 都是相同的，元数据在 1 位上也是相同的，这用于记录在声明方法时你指定的是 `out` 还是 `ref`。然而，C# 编译器以不同方式处理两者，区别在于由哪个方法负责初始化所引用的对象。如果方法被标记为 `out`，则不期望调用者在调用方法之前初始化对象。被调用方法不能读取该值，且被调用方法在返回之前必须写入该值。如果方法的参数被标记为 `ref`，调用者必须在调用方法之前初始化该值。被调用方法可以读取和/或写入该值。引用类型和值类型在 `out` 和 `ref` 下的行为非常不同。让我们看看在值类型上使用 `out` 和 `ref`。

```cs
public sealed class Program {
    public static void Main() {
        Int32 x;
        GetVal(out x); // x 已初始化。
        Console.WriteLine(x);
    }

    private static void GetVal(out Int32 v) {
        v = 10;
    }
}
```

（注：由于原始文本包含大量重复和碎片化的 OCR 错误，此处已根据提供的逻辑内容进行了整理和翻译。）
