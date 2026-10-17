
```csharp
int x = 591;
Console.WriteLine(Util.Negate(x));
```

在下面的练习中，你将为 `int` 类型添加扩展方法。通过此扩展方法，你可以将 `int` 变量的值从十进制转换为不同基数的表示形式。

# 创建扩展方法

1. 在 Visual Studio 2017 中，打开 `ExtensionMethod` 解决方案，它位于文档文件夹中的 `Microsoft Press\VCS\Chapter12ExtensionMethod` 文件夹下。

2. 在“代码和文本编辑器”窗口中显示 `Util.cs` 文件。该文件包含一个位于 `Extensions` 命名空间下的静态类 `Util`。记住你必须在静态类内部定义扩展方法。该类除了 `// TODO:` 注释外是空的。

3. 删除注释并在 `Util` 类中声明一个名为 `ToBase` 的公共静态方法。该方法应接收两个参数：名为 `i` 的 `int` 参数（带有 `this` 关键字表示它是 `int` 类型的扩展方法），以及另一个普通的 `int` 参数名为 `baseConvertToTo`。该方法将 `i` 中的值转换为 `baseConvertToTo` 指定的进制。该方法应返回一个包含转换值的 `int`。

`ToBase` 方法如下：

```csharp
static class Util
{
    public static int ConvertToBase(this int i, int baseConvertToTo)
    {
    }
}
```

4. 为 `ToBase` 方法添加 `if` 语句，检查 `baseConvertToTo` 参数的值是否在 2 到 10 之间。本练习使用的算法在该范围之外工作并不可靠。如果 `baseConvertToTo` 的值超出此范围，请抛出一个带有适当消息的 `ArgumentException`。

`ToBase` 方法如下：

```csharp
public static int ConvertToBase(this int i, int baseConvertToTo)
{
    if (baseConvertToTo < 2 || baseConvertToTo > 10)
    {
        throw new ArgumentException("Value cannot be converted to base " + baseConvertToTo.ToString());
    }
}
```

5. 将此处加粗所示的语句添加到 `ToBase` 方法中，位于抛出 `ArgumentException` 异常的语句块之后。这段代码实现了一种将数字从十进制转换为的已知算法

将 10 进制转换为不同的进制。（第 5 章“使用复合赋值和迭代语句”介绍了这种将十进制数转换为八进制的算法版本。）

点击此处查看代码图片

```csharp
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    int result = 0;
    int iterations = 0;
    do {
        int nextDigit = i % baseToConvertTo;
        i /= baseToConvertTo;
        result += nextDigit * (int)Math.Pow(10, iterations);
        iterations++;
    } While (i != 0);
    return result;
}
```

6. 在“代码和文本编辑器”窗口中显示 Program.cs 文件。

7. 在文件顶部的 `using System;` 指令之后添加以下 `using` 指令：

`using Extensions;`

此语句将包含 `Util` 类的命名空间引入作用范围。编译器可能会显示警告“Using 指令是不必要的”。然而，如果你不执行此任务，在 `Program.cs` 文件中将看不到 `ConvertToBase` 扩展方法。

8. 在 `Program` 类的 `doWork` 方法中添加以下加粗的语句，并替换 `// TODO:` 注释：

点击此处查看代码图片

```csharp
static void doWork()
{
    int x = 591;
    for (int i = 2; i <= 10; i++)
    {
        Console.WriteLine($"base is {x.ConvertToBase(i)}");
    }
}
```

此代码创建了一个名为 `x` 的 `int` 变量并将其设置为 591。（你可以选择任何需要的整数值。）然后代码使用循环打印出 2 到 10 之间所有进制的数值 591。注意，当你在 `Console.WriteLine` 语句中的 `x` 之后输入点 (`.`) 时，`ConvertToBase` 会作为扩展方法显示在 IntelliSense 中。

```csharp
namespace ExtensionMethod
{
    class Program
    {
        static void Main()
        {
            int x = 591;
            for (int i = 2; i <= 10; i++)
            {
                Console.WriteLine("%s in base %d", x.ConvertToBase(i));
            }
            try
            {
                doWork();
            } catch (Exception ex)
            {
                Console.WriteLine("Exception: %s", ex.Message);
            }
        }

    static void ConvertToBase(this int extension, int base, int baseConvertTo)
    {
        // CompareTo
        // Equals
        // GetHashCode
        // GetType
        // GetHashCode
    }
}
```

9. 在“调试”菜单上，点击“开始调试”。确认控制台显示不同进制下的数值 591，如下：

```
C:\Windows\system32\cmd.exe
591 in base 2
591 in base 3
591 in base 4
591 in base 5
591 in base 6
591 in base 7
591 in base 8
591 in base 9
591 in base 10...
```

10. 按回车键关闭程序并返回 Visual Studio。

### 总结

在本章中，你学习了如何使用继承来定义类层次结构，并且现在应该理解如何重写方法和实现虚方法。你还学习了如何为类型添加扩展方法。

- 如果你想继续，请保持 Visual Studio 运行并转到第 13 章。

- 如果你想现在退出 Visual Studio，在“文件”菜单上点击“退出”。如果看到保存对话框，点击“是”并保存项目。

### 快速参考

| 目标 | 操作 |
| :--- | :--- |
| 从基类派生类 | 声明新类名后跟冒号和基类名称。例如：[点击此处查看代码图片]<br>```class DerivedClass : BaseClass\n{\n  ...\n}``` |
| 将基类构造函数作为派生类构造函数的一部分 | 在派生类构造函数的体之前调用 base，并基构造函数提供必要的参数。例如：[点击此处查看代码图片]<br>```class DerivedClass : BaseClass\n{\n  public DerivedClass(int x) : base(x)\n  }\n}``` |
| 声明虚方法 | 在声明方法时使用 `virtual` 关键字。例如：[点击此处查看代码图片]<br>```class Mammal\n{\n  public virtual void Breathe()\n{\n  ...\n}}\``` |
| 在派生类中重写继承的虚方法 | 在派生类中声明方法时使用 `override` 关键字。例如：[点击此处查看代码图片]<br>```class Whale : Mammal\n{\n    public override void Breathe()\n        ...\n    }\n}``` |
| 为类型定义扩展方法 | 向静态类添加静态公共方法。第一个参数必须是被扩展的类型，并由 `this` 关键字引导。例如：[点击此处查看代码图片]<br>```static class Util\n{\n    public static int Negate(this int i)\n{\n        return -i;\n    }\n}``` |

### 创建接口和定义抽象类

完成本章后，你将能够：

- 定义指定方法签名和返回类型的接口。
- 在结构或类中实现接口。
- 通过接口引用类。
- 在抽象类中捕实现细节。
- 实现无法派生新类的密封类。

继承类是一种强大的机制，但继承真正的力量来自于继承接口。接口不包含任何代码或数据；它只是指定了继承接口的类必须提供的方法和属性。通过使用接口，你可以将类的方法和签名与方法的实现完全分离。

抽象类在许多方面与接口相似，但抽象类可以包含代码和数据。然而，你可以将抽象类的某些方法指定为虚方法，以便继承抽象类的类可以选择提供自己的实现。你经常将抽象类与接口配合使用，它们共同提供了一种你可以构建可扩展编程框架的关键技术，你将在章节中发现。

### 理解接口

假设你想定义一个新的类，在其中存储对象集合，就像使用数组一样。然而，与数组不同，你希望提供一个名为 `RetrieveInOrder` 的方法，允许应用程序按对象类型检索对象。例如，如果集合包含字母数字对象（如字符串），集合应该允许应用程序根据计算机的排序顺序顺序检索这些字符串；如果集合包含数值对象（如整数），集合应该允许应用程序按数字顺序检索对象。

当你定义集合类时，你不想限制它所容纳的对象类型（对象可以是类或结构体类型），因此你不知道如何对这些对象排序。那么，你如何为集合类提供一个在实际检索集合时对未知类型对象进行排序的方法呢？乍一看，这个问题似乎与第 12 章“使用继承”中描述的 ToString 问题相似，可以通过创建一个允许集合类的子类重写的虚方法来解决。然而，任何相似性都是误导性的。集合类与其持有的对象之间没有继承关系，因此虚方法将毫无用处。如果你想一下，问题在于集合中对象的排序方式取决于对象本身的类型，而不是取决于集合本身。解决方案是要求所有对象都提供一个方法（例如示例中的 `CompareTo` 方法），供集合的 `RetrieveInOrder` 方法调用，从而使集合能够对这些对象进行比较：

点击此处查看代码图片

```
int CompareTo(object obj)
{
// 如果此实例等于 obj 则返回 0
// 如果此实例小于 obj 则返回负数
// 如果此实例大于 obj 则返回正数
}
```

你可以为可集合对象定义一个接口，该接口包含

`CompareTo` 方法并指定接口只能包含实现此的类。通过这种方式，接口类似于一个契约。如果一个类实现了接口，接口保证该类包含了接口中指定的所有方法。

使用接口，你可以真正将“做什么”与“怎么做”分开来。接口提供了方法的名称、返回类型和参数。至于方法具体是如何实现的并不是接口关心的范围。

### 定义接口

定义接口在语法上与定义类相似，只不过你使用 `interface` 关键字而不是 `class` 关键字。在接口内部，你像类或结构体一样声明方法，只不过你不需要指定访问修饰符（如 `public`、`private` 或 `protected`）。此外，接口中的方法没有实现；它们只是声明，所有实现接口的类型必须提供自己的实现。因此，你用分号替换方法体。这是一个示例：

点击此处查看代码

```
interface IComparable
{
    int CompareTo(object obj);
}
```

> Tip .NET Framework 文档建议接口名称以大写字母 I 开头。这是匈牙命名法在 C# 中最后的遗迹。顺便说，System 命名空间已经定义了 `IComparable` 接口如下：

接口不能包含任何数据；你不能向接口添加字段（即使是私有字段）。

### 实现接口

要实现接口，你需要声明一个继承该接口并实现接口指定的所有方法的类或结构体。这并不是真正的继承，尽管语法是相同的，你将在本章后面的部分看到许多继承的特征。你应该注意，与类继承不同，结构体可以实现接口。

例如，假设你正在定义第 12 章描述的 `Mammal`（哺乳动物）层级。你需要指定陆栖动物提供一个名为 `NumberOfLegs` 的方法。（海栖动物不实现此接口。）你可以如下定义 `ILandBound` 接口，它包含该方法：

点击此处查看代码

```csharp
interface ILandBound
{
    int NumberOfLegs();
}
```

你可以在 `Horse` 类中实现这个接口。继承接口并提供接口定义的每个方法的实现（在这种情况下，只有一个方法 `NumberOfLegs`）。

点击此处查看代码

```csharp
class Horse : ILandBound
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

当你实现接口时，你必须根据以下规则确保每个方法与其接口方法完全匹配：

- 方法名和返回类型完全匹配。
- 任何参数（包括 `ref` 和 `out` 关键字修饰符）完全匹配。
- 所有实现接口的方法必须是公共的。但是，如果你使用显式接口实现，方法不应该有访问限定符。

如果接口定义与其声明实现之间存在任何差异，类将无法编译。

> Tip Microsoft Visual Studio 开发环境（IDE）可以帮助减少因未能实现接口方法而导致的错误。“实现接口”向导可以为类实现的接口中的每个项目生成存根（stubs）。然后你用适当的代码填充这些存根。你将在本章后面的练习中看到如何使用此向导。

一个类可以同时继承另一个类并实现接口。在这种情况下，C# 不像 Java 那样使用特定的关键字来区分基类和接口。相反，C# 使用位置表示法。基类始终第一个命名，后面跟着一个逗号，然后是接口。接下来的示例定义 `Horse` 是一个 `Mammal` 类，但额外实现了 `ILandBound`

点击此处查看代码

```csharp
interface ILandBound
{
}
class Mammal
{
}
class Horse : Mammal, ILandBound
{
}
```

## 通过接口引用类

请注意，接口 `InterfaceA` 可以继承另一个接口 `InterfaceB`。技术上，这被称为接口扩展而不是继承。在这种情况下，任何实现 `InterfaceA` 的类或结构体都提供 `InterfaceB` 和 `InterfaceA` 中所有方法的实现。

就像通过定义为更高层次类的变量来引用对象一样，你也可以通过定义为对象类实现的接口变量来引用对象。以之前的示例为例，你可以使用 `ILandBound` 变量来引用 `Horse` 对象，如下：

点击此处查看代码

```csharp
Horse myHorse = new Horse(...);
ILandBound landBound = myHorse;
```

所有的 Horse 都是 `ILandBound`，但反之并不成立——你不能在不进行转换的情况下将 `ILandBound` 对象赋值给 `Horse` 变量。

通过接口引用对象是有用的，因为你可以处理实现了该接口的不同类型。例如，在第 8 章“理解值和引用”中演示了如何使用 `is` 运算符来检查对象是 `ILandBound` 的实例：

点击此处查看代码

```csharp
if (myHorse is ILandBound)
{
    ILandBound landBound = myHorse;
}
```

实现，因此相同的方法实际上同时实现了两个接口。

为了解决这个问题并区分哪种方法属于哪个接口实现，你可以显式地实现接口。要实现这一点，你可以在实现方法时指定该方法属于哪个接口，如下：

点击此处查看代码图像

```
class Horse : ILandBound, IJourney
{
  ...
  int ILandBound.NumberOfLegs()
{
    return 4;
  }
  int IJourney.NumberOfLegs()
{
    return 3;
  }
}
```

你可以看到马有四条腿，并且在旅程中拉了三条腿长度的车车。

除了在名称前加上接口名称之外，这种语法中还有一个细微的差别：方法没有标记为 `public`。你不能为属于显式接口实现的方法指定访问修器。这导致了另一个有趣的现象。如果你在代码中创建一个 `Horse` 变量，你实际上无法调用任何一个 `NumberOfLegs` 方法，因为它们是不可可见的。对于 `Horse` 类而言，它们都是私有的。事实上，这是合理的。如果方法通过 `Horse` 类可见，那么以下代码实际上会调用哪一个方法呢？是 `ILandBound` 接口的还是 `IJourney` 的？

点击此处查看代码图像

```
Horse horse = new Horse();
...
// 下述语句无法编译
```
