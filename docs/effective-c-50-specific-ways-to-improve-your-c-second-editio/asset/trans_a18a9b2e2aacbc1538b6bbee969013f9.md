

避免代码重复，并且构造函数初始化器会生成更高效的对象代码。C# 编译器将构造函数初始化器识别为特殊语法，并删除重复的变量初始化器和重复的基类构造函数调用。结果是你的最终对象执行最少量的代码来正确初始化对象。你也可以通过将职责委托给一个公共构造函数来编写最少的代码。

构造函数初始化器允许一个构造函数调用另一个构造函数。以下示例展示了简单的用法：

```
public class MyClass
{
    // collection of data
    private List<ImportantData> coll;
    // Name of the instance:
    private string name;

    public MyClass() :
        this(0, "")
    {
    }

    public MyClass(int initialCount) :
        this(initialCount, string.Empty)
    {
    }

    public MyClass(int initialCount, string name)
    {
        coll = (initialCount > 0) ?
            new List<ImportantData>(initialCount) :
            new List<ImportantData>();
        this.name = name;
    }
}
```

C# 4.0 添加了默认参数，你可以使用它来最小化构造函数中的重复代码。你可以用一个指定所有或许多值默认值 的构造函数替换 MyClass 的所有不同构造函数：

```
public class MyClass
{
    // collection of data
    private List<ImportantData> coll;
    // Name of the instance:
    private string name;

    // Needed to satisfy the new() constraint.
    public MyClass() :
        this(0, string.Empty)
    {
    }

    public MyClass(int initialCount = 0, string name = "")
    {
        coll = (initialCount > 0) ?
            new List<ImportantData>(initialCount) :
            new List<ImportantData>();
        this.name = name;
    }
}
```

在选择默认参数而不是使用多个重载时存在权衡。 （参见第 10 条。）默认参数为你的用户提供了更多选项。MyClass 的这个版本为两个参数都指定了默认值。用户可以为一个或两个参数指定不同的值。使用重载构造函数生成所有排列将需要四个不同的构造函数重载：一个无参数构造函数、一个要求初始计数的构造函数、一个要求名称的构造函数，以及一个要求两个参数的构造函数。向你的类添加更多成员时，潜在的重载数量会随着所有参数的排列数量的增加而增长。这种复杂性使得默认参数成为最小化你需要创建的潜在重载数量的非常强大的机制。

为你的类型的构造函数的所有参数定义默认值意味着当你调用 new MyClass() 时用户代码将有效。当你打算支持此概念时，你应该在该类型中创建一个显式的无参数构造函数，如上面的示例代码所示。虽然大多数代码会为所有参数设置默认值，但使用 new() 约束的泛型类不会接受所有参数都有默认值的构造函数。为了满足 new() 约束，一个类必须有一个显式的无参数构造函数。因此，你应该创建一个，以便客户端可以在强制执行 new() 约束的泛型类或方法中使用你的类型。这并不意味着每种类型都需要一个无参数构造函数。然而，如果你支持它，请确保添加代码以使无参数构造函数在所有情况下都能工作，即使是从具有 new() 约束的泛型类调用。

你会注意到第二个构造函数为 name 参数指定了 "" 作为默认值，而不是更常见的 string.Empty。这是因为 string.Empty 不是编译时常量。它是在 string 类中定义的静态属性。由于它不是编译时常量，因此你不能将其用于参数的默认值。

然而，使用默认参数而不是重载会使你的类与使用它的所有客户端之间产生更紧密的耦合（参见第 10 条）。特别是，形式参数名称成为公共接口的一部分，当前默认值也是如此。更改参数值需要重新编译所有客户端代码以获取这些更改。这使得重载构造函数在面对潜在的未来更改时更具弹性。你可以添加新的构造函数，或更改不指定值的那些构造函数的默认行为，而不会破坏客户端代码。

C# 1 到 3 版本不支持默认参数，这是解决此问题的首选方案。你必须将支持的每个构造函数作为单独的函数编写。对于构造函数来说，这可能意味着大量重复的代码。使用构造函数链，通过让一个构造函数调用同一类中声明的另一个构造函数，而不是创建公共实用例程。 在这种分解公共构造函数逻辑的替代方法中存在几种低效率：

```
public class MyClass
{
    // collection of data
    private List<ImportantData> coll;
    // Name of the instance:
    private string name;

    public MyClass()
    {
        commonConstructor(0, "");
    }

    public MyClass(int initialCount)
    {
        commonConstructor(initialCount, "");
    }

    public MyClass(int initialCount, string Name)
    {
        commonConstructor(initialCount, Name);
    }

    private void commonConstructor(int count,
        string name)
    {
        coll = (count > 0) ?
            new List<ImportantData>(count) :
            new List<ImportantData>();
        this.name = name;
    }
}
```

该版本看起来相同，但生成的对象代码效率远低于前者。编译器会在构造函数中代表你添加代码来执行多个功能。它为所有变量初始化器添加语句（参见第 12 条）。它调用基类构造函数。当你编写自己的公共实用函数时，编译器无法分解这种重复代码。第二个版本的 IL 与你编写以下内容相同：

```
// Instance Initializers would go here.
object(); // Not legal, illustrative only.
commonConstructor(initialCount, "");
}
```

```
public MyClass(int initialCount)
{
    // Call the third constructor, shown below.
    this(initialCount, "");
}

public MyClass(int initialCount, string Name)
{
    // Instance Initializers would go here.
    object(); // Not legal, illustrative only.
    coll = (initialCount > 0) ?
        new List<ImportantData>(initialCount) :
        new List<ImportantData>();
    name = Name;
}
```

区别在于编译器不会生成对基类构造函数的多次调用，也不会将实例变量初始化器复制到每个构造函数体中。基类构造函数仅从最后一个构造函数调用这一事实也很重要：你不能在一个构造函数定义中包含多个构造函数初始化器。你可以使用 this() 委托给此类中的另一个构造函数，或使用 base() 调用基类构造函数。你不能同时做两者。

仍然不相信构造函数初始化器的案例？那么想想只读常量。在此示例中，对象的名称在其生命周期内不应更改。这意味着你应该使其为只读。这会导致公共实用函数生成编译器错误：

```
public class MyClass
{
    // collection of data
    private List<ImportantData> coll;
    // Number for this instance
    private int counter;
    // Name of the instance:
    private readonly string name;

    public MyClass()
    {
        commonConstructor(0, string.Empty);
    }
}
```
