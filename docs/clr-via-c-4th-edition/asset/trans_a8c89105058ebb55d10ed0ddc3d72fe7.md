

> **注意** `ExtensionAttribute` 类定义在 `System.Core.dll` 程序集中。这意味着，即使我不使用 `System.Core.dll` 中的任何类型，甚至编译代码时根本不引用 `System.Core.dll`，编译器生成的程序集中仍会嵌入对 `System.Core.dll` 的引用。不过，这不算太糟糕，因为 `ExtensionAttribute` 只在编译时使用；在运行时，除非应用程序使用此程序集中的其他内容，否则不必加载 `System.Core.dll`。

## 部分方法

想象你使用一个工具生成包含类型定义的 C# 源代码文件。该工具知道在其生成的代码中有一些潜在位置，你可能想在这些位置自定义类型的行为。通常，自定义会通过让工具生成的代码调用虚方法来完成。工具生成的代码还必须包含这些虚方法的定义，而这些方法的实现方式是什么也不做并直接返回。现在，如果你想自定义类的行为，你会定义自己的类，从基类派生，然后重写实现该行为的任何虚方法，使其具有你想要的行为。下面是一个示例。

```csharp
// Tool-produced code in some source code file:
internal class Base {
    private String m_name;

    // Called before changing the m_name field
    protected virtual void OnNameChanging(String value) {
    }

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper());  // Inform class of potential change
            m_name = value;                   // Change the field
        }
    }
}

// Developer-produced code in some other source code file:
internal class Derived : Base {
    protected override void OnNameChanging(String value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

不幸的是，前面的代码有两个问题：

- 类型必须是非密封类。不能对密封类或值类型使用此技术（因为值类型隐式密封）。此外，不能对静态方法使用此技术，因为静态方法不能被重写。
- 这里存在效率问题。定义类型只是为了重写一个方法；这会浪费少量系统资源。而且，即使你不想重写 `OnNameChanging` 的行为，基类代码仍然会调用一个只做返回、什么也不做的虚方法。另外，无论 `OnNameChanging` 是否访问传给它的参数，都会调用 `ToUpper`。

C# 的部分方法特性允许你选择重写类型行为，同时解决上述问题。下面的代码使用部分方法实现与前面代码相同的语义。

```csharp
// Tool-produced code in some source code file:
internal sealed partial class Base {
    private String m_name;

    // This defining-partial-method-declaration is called before changing the m_name field
    partial void OnNameChanging(String value);

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper()); // Inform class of potential change
            m_name = value;                  // Change the field
        }
    }
}

// Developer-produced code in some other source code file:
internal sealed partial class Base {
    // This implementing-partial-method-declaration is called before m_name is changed
    partial void OnNameChanging(String value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

关于这个新版本代码，有几点需要注意：

- 该类现在是密封的（尽管它不必是）。事实上，该类可以是静态类，甚至是值类型。
- 工具生成的代码和开发者编写的代码实际上是两个部分定义，最终组成一个类型定义。有关部分类型的更多信息，请参阅第 6 章“类型和成员基础”中的“部分类、结构和接口”一节。
- 工具生成的代码定义了一个部分方法声明。此方法用 `partial` 标记，并且没有方法体。
- 开发者编写的代码实现了该部分方法声明。此方法也用 `partial` 标记，并且有方法体。

> **注意** 在 Visual Studio 编辑器中，如果你输入 `partial` 并按空格键，IntelliSense 窗口会显示当前封闭类型中已定义但还没有匹配实现部分方法声明的所有部分方法声明。然后，你可以轻松地从 IntelliSense 窗口中选择一个部分方法，Visual Studio 会自动为你生成方法原型。这是一个非常好的功能，可以提高工作效率。

但是，部分方法还带来了另一个重大改进。假设你不需要修改工具生成的类型的行为。在这种情况下，你根本不提供源代码文件。如果你只单独编译工具生成的代码，编译器生成的 IL 代码和元数据就如同工具生成的代码如下所示。

```csharp
// Logical equivalent of tool-produced code if there is no
// implementing partial method declaration:
internal sealed class Base {
    private String m_name;

    public String Name {
        get { return m_name; }
        set {
            m_name = value;              // Change the field
        }
    }
}
```

也就是说，如果没有实现部分方法声明，编译器不会发出任何表示该部分方法的元数据。此外，编译器不会发出任何 IL 指令来调用该部分方法。并且，编译器不会发出代码来计算原本会传递给该部分方法的任何参数。在此示例中，编译器不会发出调用 `ToUpper` 方法的代码。结果是更少的元数据/IL，并且运行时性能非常棒！

> **注意** 部分方法的工作方式类似于 `System.Diagnostics.ConditionalAttribute` 特性。但是，部分方法仅在一个类型内起作用，而 `ConditionalAttribute` 可用于选择性地调用另一个类型中定义的方法。

### 规则与准则

关于部分方法，还有一些额外的规则和准则你应该知道：

- 它们只能在部分类或部分结构中声明。
- 部分方法必须始终具有 `void` 返回类型，并且不能有任何用 `out` 修饰符标记的参数。这些限制存在的原因是，在运行时该方法可能不存在，因此你不能将变量初始化为该方法可能返回的值，因为该方法可能不存在。同样，也不能有 `out` 参数，因为该方法必须初始化它，而该方法可能不存在。部分方法可以有 `ref` 参数，可以是泛型的，可以是实例方法或静态方法，并且可以标记为 `unsafe`。
- 当然，定义部分方法声明和实现部分方法声明必须具有完全相同的签名。如果两者都应用了自定义特性，则编译器会将两个方法的特性合并在一起。应用于参数的任何特性也会合并。
- 如果没有实现部分方法声明，那么你不能有任何代码试图创建引用该部分方法的委托。原因同样是该方法在运行时不存在。编译器会生成以下消息：`error CS0762: Cannot create delegate from method 'Base.OnNameChanging(String)' because it is a partial method without an implementing declaration.`
- 部分方法始终被视为私有方法。但是，C# 编译器禁止你在部分方法声明前放置 `private` 关键字。

