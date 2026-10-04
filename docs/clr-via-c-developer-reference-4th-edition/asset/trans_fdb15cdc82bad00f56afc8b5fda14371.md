

> 注意：ExtensionAttribute 类定义在 System.Core.Dll 程序集中。这意味着，即使我在编译代码时没有使用 System.Core.Dll 中的任何类型，甚至没有引用 System.Core.Dll，编译器生成的程序集也将包含一个对 System.Core.Dll 的引用。不过，这并不是太严重的问题，因为 ExtensionAttribute 仅在编译时使用；在运行时，除非应用程序消耗某些内容，否则不需要加载 System.Core.Dll。

## 部分方法 (Partial Methods)

假设你正在使用一个工具，它可以生成一个包含类型定义的 C# 源代码文件。该工具知道在其生成的代码中存在某些潜在的地方，你可能希望在那里自定义类型的行为。通常情况下，自定义是通过让工具生成的代码调用方法来实现的。工具生成的代码还必须包含这些虚方法的定义，并且这些方法的实现方式将是什么都不做并直接返回。现在，如果你想自定义类的行为，可以定义你自己的类，继承自基类，并重写任何虚方法，使其具有你所需的行为。这里是一个示例。

```csharp
// 某些源文件中工具生成的代码：
internal class Base {
    private String m_name;

    // 在更改 m_name 字段之前
    protected virtual void OnChanging(String value);

    public String Name {
        get { return m_name; }
        set {
            OnChanging(value); // 通知类可能发生的更改
            m_name = value; // 更改字段
        }
    }
}
```

```csharp
// 另一个源文件中开发者生成的代码：
internal class Derived : Base {
    protected override void OnChanging(string value) {
        if (String.IsNullOrEmpty(value)) {
            throw new ArgumentNullException("value");
        }
    }
}
```

遗憾的是，上述代码存在两个问题：

- 该类型必须是非密封的（not sealed）的类。你不能对密封类或值类型使用此技术（因为值类型是隐式密封的）。此外，你还不能将此技术用于静态方法，因为静态方法无法被重写。
- 这里存在效率问题。为了重写一个方法而定义一个类型会浪费了系统资源。而且，即使你不想重写 OnChanging 的行为，基类仍然会调用一个除了返回之外无所事事的虚方法。此外，无论是否传递了参数，OnChanging 都会被调用。

C# 部分方法允许你在修复上述问题的同时，获得自定义类型行为的选择。下面的代码使用部分方法实现了与之前代码相同的功能。

```csharp
// 某些源文件中工具生成的代码：
internal class Base {
    private String m_name;

    // 部分方法声明在更改 m_name 字段之前调用
    partial void OnChanging(String value);

    public String Name {
        get { return m_name; }
        set {
            OnChanging(value); // 通知类可能发生的更改
            m_name = value; // 更改字段
        }
    }
}
```

```csharp
// 另一个源文件中开发者生成的代码：
internal class Base {
    // 在 m_name 更改之前调用部分方法方法的实现
    partial override void OnChanging(String value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

关于这个版本的代码有几点需要注意：

- 类现在是密封的（sealed）（尽管它不必是密封的）。实际上，该类可以是静态类，甚至是值类型。
- 工具生成的代码和开发者生成的代码实际上是最终构成一个类型的两个定义。关于部分类型（partial types）的更多信息，请参见第 6 章中的“部分类、结构体和接口”部分。
- 工具生成的代码定义了一个部分方法声明。该方法标记了 `partial` 且没有方法体。
- 开发者生成的代码实现了方法声明。该方法也标记了 `partial` 标记并具有方法体。

现在当你编译它时，你将看到与原始代码相同的效果。同样，这里的巨大优势在于可以在单独的文件中生成新代码，但你的代码不受影响。而且，这种技术适用于密封类、静态类和值类型。

> 注意：在 Visual Studio 的编辑器中，如果你输入 `partial` 并按下空格键，IntelliSense 窗口会向你显示包含类型定义的所有尚未匹配方法声明的部分方法声明。你可以轻松地从 IntelliSense 窗口选择一个部分方法，Visual Studio 将为你生成方法原型。这是一个增强生产力的极佳功能。

但是，部分方法还有另一个巨大的改进。假设你不需要修改工具生成类型的行为。在这种情况下，你完全不需要提供源代码。如果你单独编译工具生成的代码，编译器将生成 IL 代码和元数据，就像工具生成的代码如下所示：

```csharp
// 如果没有实现部分方法声明，工具生成代码的逻辑如下：
internal class Base {
    private String m_name;

    public String Name {
        get { return m_name; }
        set {
            m_name = value; // 更改字段
        }
    }
}
```

也就是说，如果没有实现部分方法声明，编译器将不会产生表示该部分的元数据。此外，编译器不会生成调用部分方法的 IL 指令。而且，编译器不会生成评估可能传递给部分方法的任何参数的代码。在这个示例中，编译器不会生成调用 `ToUpper` 方法的代码。结果是减少了元数据/IL，并且运行时性能非常出色！

> 注意：部分方法的工作原理与 `System.Diagnostics.ConditionalAttribute` 属性类似。然而，部分方法在单个类型内部工作，而 `ConditionalAttribute` 可用于可选地调用另一个类型的方法。

## 规则与指南 (Rules and Guidelines)

关于部分方法，你还需要了解一些额外的规则和指南：

- 它们只能在部分类（partial class）或部分结构体（partial struct）中声明。
- 部分方法必须始终返回 `void` 类型，且不能有任何标记为 `out` 修饰符的参数。设置这些限制是因为在运行时，方法可能不存在，因此你无法根据方法的可能返回值来初始化变量。同样，你不能有 `out` 参数，因为方法必须初始化它，而该方法可能不存在。部分方法可以有 `ref` 参数，可以是实例方法或静态方法，并且可以标记为 `unsafe`。
- 当然，定义部分方法声明和实现部分方法声明必须具有相同的签名。如果两者都应用了自定义属性，编译器将合并两个方法的属性。应用到参数上的任何属性也会被合并。
- 如果没有实现部分方法声明，则你不能有任何尝试引用该部分方法的委托代码。再次，原因是该方法在运行时不存在。编译器会产生此错误信息：错误 CS0762：无法从方法 'Base.OnChanging(string)' 创建委托，因为它是一个没有实现声明的部分方法。

