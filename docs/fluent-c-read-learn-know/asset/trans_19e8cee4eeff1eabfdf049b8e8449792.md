

## 构建构造函数

最佳实践规定构造函数应做得很少。事实上，大多数设计良好的构造函数仅使用属性访问器将类属性设置为初始值，以确保进行任何必要的验证。

你应该使用属性访问器的原因是为了避免重复代码。重复代码总是不好的。（至少，在我多年的编程生涯中，我从未见过这样做的充分理由。如果你想到了，请给我发邮件。）这同样适用于构造函数，如同应用程序中的其他任何地方一样。

这里存在一个冲突：一方面，在实例化对象时只能设置对象的基本属性，对你的类的用户来说是一种善意，这通常意味着构造函数有多个重载。另一方面，你不希望在各种方法调用中重复设置这些属性的代码。解决方案是使用一种称为构造函数链的设计模式：参数较少的构造函数版本调用参数较多的版本，为缺失的参数提供合理的默认值：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_270_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_270_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_271_0.png)

## 戴上你的思考帽

我们示例应用程序中的 Ingredient 类是尝试编写构造函数技能的好地方。添加两个构造函数：一个允许用户设置 Name 属性，另一个不接受任何参数（换句话说，默认构造函数）。

（答案在第 265 页。）

## 作用域

当你使用声明语句创建变量时，.NET 会分配足够的内存来存储指定类型的属性，并使你声明的标识符可供使用。但声明的元素不会永久存在，你也不能从任何地方访问它们。规则很简单：变量仅在其定义的上下文中可见。这是一条简单的规则，让我们看一个简单的示例：

public 关键字只能应用于类型和成员，不能应用于变量。

```csharp
public class MyClass
{
    public void MyMethod()
    {
        String Sentence = "My name is ";
    }

    public string MySentence(string Name)
    {
        return Sentence += Name;
    }
}
```

变量 Sentence 在 MyMethod 内定义。这就是它的作用域。它不能声明为 public。

尽管它们在同一个类定义中声明，MySentence 也看不到变量 Sentence，因为它是在不同的作用域中声明的。

```csharp
MyClass MakeAName = new MyClass;
MessageBox.Show(MyClass.Sentence);
```

调用代码看不到在 MyMethod 内声明的变量 Sentence。

## 你做得怎么样？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_273_0.png)

默认构造函数只是将默认值传递给重载。

```csharp
public Ingredient()
{
    this.Ingredient("No Name");
}
```

重载使用公共属性的 set 访问器来设置 Name。

```csharp
public Ingredient(String name)
{
    this.Name = name;
}
```

## 戴上你的思考帽

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_273_1.png)

作用域确实是一个相当简单的原则，但有几个地方你可能会让自己混淆。让我们看看两个最常见的：

```csharp
public class MyClass
{
    private Int32 x = 5;

    public void DoSomething()
    {
        Int32 x = 0;
        MessageBox.Show(x.ToString());
    }

    public void DoSomethingElse()
    {
        for (Int32 y; y <= 5; y++)
        {
            x++;
        }
        MessageBox.Show(y.ToString());
    }
}
```

MessageBox 中会显示什么？

这一行为什么会失败？

## 你做得怎么样？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_274_0.png)

```csharp
public class MyClass
{
    private Int32 x = 5;

    public void DoSomething()
    {
        Int32 x = 0;
        MessageBox.Show(x.ToString());
    }

    public void DoSomethingElse()
    {
        for (Int32 y; y <= 5; y++)
        {
            x++;
        }
        MessageBox.Show(y.ToString());
    }
}
```

MessageBox 将显示 0，因为方法内部声明的变量隐藏了外部声明的变量。如果你想显示 5，则需要使用 this 关键字，但可以肯定的是，如果存在混淆的可能，避免使用重复的变量名确实是最佳实践。

这一行会失败，因为 y 在 for 语句的上下文中声明，而不是在方法本身中。当 for 语句退出时，y 会超出作用域。

## 最佳实践 — 变量名

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_274_1.png)

警告：变量名 a、b、c 和 x、y、z 很危险。习惯上将它们用作循环的控制变量，就像我在这里所做的那样，但它们除了告诉你它们是控制变量之外，什么也说明不了。如果你打算将它们用于其他任何目的，你应该选择一个更具描述性的名称（即使只是 loopCounter）。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_275_0.png)

## 显微镜下——垃圾回收

你知道，当你声明一个变量时，.NET 会为其分配内存。当变量超出作用域时，该内存不再需要，可供重用，这个过程称为垃圾回收。请注意，我说的是可供“重用”，而不是“已重用”。

在旧的编程语言中，内存会立即被回收，但 .NET Framework 使用更复杂的过程：非确定性垃圾回收。系统不会在回收它可能永远不需要的内存时停止一切（默认情况下，.NET Framework 应用程序有 2 GB 的内存可供变量使用；这是很多变量），垃圾回收器会跟踪在需要时可以回收的内容，并且只有在必要时才会重新组织事物。它在应用程序没有做其他事情时（例如，在等待用户输入时）进行内部维护也相当聪明。

在绝大多数情况下，垃圾回收工作正常，你无需考虑它，但 .NET Framework 确实在你需要时（以及如果你需要时）为你提供了一些对该过程的控制。有关详细信息，请查看 MSDN 上的“垃圾回收”（在你需要时，以及如果你需要时）。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_275_1.png)

## 休息一下

我们将在后续内容中探讨方法的其他方面和其他类别的方法，但暂时就到这里。在做最终的复习练习之前，为什么不休息一下呢？

## 复习

这是一个表示 Neil & Gordon 咖啡馆原料供应商的简单类的类图。编写类代码。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_276_0.png)

## 恭喜！你已完成本章。在进入下一章之前，花一分钟思考一下你所取得的成就...

列出你在本章学到的三件事：

- 1
- 2
- 3

你认为为什么需要知道这些东西才能成为一名 C# 程序员？

本章中有什么你觉得需要更详细理解的内容吗？如果有，你打算怎么做？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_278_0.png)

## 其他框架类型

在上一章中，我们探讨了如何定义 .NET Framework 类。类是框架类型中最常见的，在很多方面也是最复杂的，但它们不是唯一的类型。在本章中，我们将探讨剩余的类型：结构体，类似于小型类；枚举，是简单的值列表；接口，类似于没有任何实现的类定义。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_279_0.png)

## 将其纳入

与类一样，结构体、枚举和接口是使用 C# 类型和成员关键字（其中许多你已经知道）实现的，并最终被翻译成 .NET Framework CTS（公共类型系统）类型。在本章中，我们将探讨这些剩余类型，以及它们如何融入 CTS。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_280_0.png)

与类一样，类型在 C# 中使用类型关键字定义。

编译器将 C# 类型翻译成 .NET Framework 类型。

在运行时，CLR 将 .NET Framework 类型翻译成公共类型系统类型。

