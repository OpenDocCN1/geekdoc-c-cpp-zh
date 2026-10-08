
尽管字符串插值几乎已经让这个版本的 `WriteLine` 方法变得多余，但该重载在 C# 语言之前的版本中被频繁使用。该重载使 `WriteLine` 方法支持包含数字占位符的格式字符串参数，每个占位符在运行时都可以被参数列表中指定的任意类型的变量替换（占位符被其后列表列表中第 $i$ 个变量替换）。以下是调用该方法的示例（变量 `fname` 和 `iname` 是字符串，`mi` 是 `char`，`age` 是 `int`）：

点击此处查看代码图片

```cs
Console.WriteLine("Forename:, Middle Initial:, Last name:, Age:", fname, mi, Iname, age);
```

编译器将此调用解析为：

点击此处查看代码图片

```cs
Console.WriteLine("Forename:, Middle Initial:, Last name:, Age:", new object[4]{fname, mi, Iname, age});
```

### 使用 params 数组

在下面的练习中，你将实现并测试一个名为 `Sum` 的静态方法。该方法的目的是计算传递给它的任意数量 `int` 参数之和，并将结果作为 `int` 返回。你将通过编写 `Sum` 接收一个 `params int[]` 参数来实现。你将对 `params` 参数进行两次检查，以确保 `Sum` 方法完全健壮。然后，你将使用各种不同的参数调用 `Sum` 方法对其进行测试。

### 编写一个 params 数组方法

1. 启动 Microsoft Visual Studio 2017（如果它尚未运行）。
2. 打开 `ParamsArray` 解决方案，它位于 `\Microsoft Press\VCSBS\Chapter 11\ParamsArray` 文件夹下。
3. `ParamsArray` 项目包含 `Program.cs` 文件中的 `Program` 类，包括你在之前的章节中看到的 `doWork` 框架。你将 `Sum` 方法实现为另一个名为 `utility` 的类的静态方法，你将将其添加到项目中。
4. 在解决方案管理器中，右键点击 `ParamsArray` 解决方案中的 `ParamsArray` 项目，指向“添加”，然后点击“类”。
5. 在“添加项—ParamsArray”对话框中，在中间面板中，点击“类”模板。在“名称”框中输入 `Util.cs`，然后点击“添加”。

`Util.cs` 文件已创建并添加到项目中。它包含一个位于 `ParamsArray` 命名空间下的名为 `Util` 的空类。

点击此处查看代码图片

```cs
public static int Sum(params int[] paramList)
{}
```

```c
int sumTotal = 0;
}
```

+ 9. 在 `Sum` 方法中添加 `foreach` 语句以遍历 `paramList` 数组。该 `foreach` 循环的主体应将数组中的每个元素添加到 `sumTotal`。在方法的结束处，使用 `return` 语句返回 `sumTotal` 的值，如此处加粗处所示：

点击此处查看代码图像

```c
public static int Sum(params int[] paramList)
{
  int sumTotal = 0;
  foreach (int i in paramList)
  {
    sumTotal += i;
  }
  return sumTotal;
}
```

+ 10. 在 生成 菜单上，点击 生成解决方案，然后确认解决方案在没有任何错误的情况下生成。

### 测试 Util.Sum 方法

+ 1. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。
+ 2. 在代码和文本编辑器窗口中，删除 `// TODO:` 注释并在 `doWork` 方法中添加以下语句：

点击此处查看代码图像

```c
Console.WriteLine(Util.Sum(null));
```

+ 3. 在 调试 菜单上，点击 无带调试启动。

程序编译并运行，在控制台中输出以下消息：

点击此处查看代码图像

Exception: Util.Sum: null parameter list

这确认了方法中的第一个检查有效。

+ 4. 按回车键关闭程序并返回到 Visual Studio 2017。
+ 5. 在代码和文本编辑器窗口中，如下所示更改 `doWork` 中对 `Console.WriteLine` 的调用：

```c
Console.WriteLine(Util.Sum());
```

这一次，调用方法时没有传递任何参数。编译器将空参数列表转换为一个空数组。

+ 在 调试 菜单上，点击 无带调试启动。

程序编译并运行，在控制台中输出以下消息：

点击此处查看代码图像

Exception: Util.Sum: empty parameter list

这确认了方法中的第二个检查有效有效。

+ 按回车键关闭程序并返回到 Visual Studio 2017。
+ 按照如下方式更改 `doWork` 中对 `Console.WriteLine` 的调用：

点击此处查看代码图像

```c
Console.WriteLine(Util.Sum(10, 9, 8, 7, 6, 5, 4, 3, 2, 1));
```

+ 在 调试 菜单上，点击 无带调试启动。

验证程序是否编译、运行，并向控制台输出值 55。

+ 按回车关闭应用程序并返回到 Visual Studio 2017。

### 比较参数数组和可选参数

第 3 章“编写方法和应用作用域”阐述了如何定义接收可选参数的方法。从表面上看，使用参数数组的方法与接收可选参数的方法之间似乎存在某种程度的重叠。然而，它们之间存在根本性的区别：

+ 接收可选参数的方法仍然有一个固定的参数列表，你不能传递任意的参数列表。编译器会生成代码，在方法运行之前将任何缺失参数的默认值插入到栈中，而且方法本身并无法感知哪些参数是调用者提供的，哪些是编译器生成的默认值。
+ 使用参数数组的方法实际上拥有一个完全任意的参数列表，且其中任何一个参数都没有默认值。此外，方法可以确切地确定调用者提供了多少个参数。

```c
class Util
{
    public static int Sum(int param1 = 0, int param2 = 0, int param3 = 0, int param4 = 0)
    {
        Console.WriteLine("Using optional parameters");
        int sumTotal = param1 + param2 + param3 + param4;
        return sumTotal;
    }
}
```

4. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。
5. 在 `doWork` 方法中，注释掉现有的代码然后添加以下语句：

点击此处查看代码图像

```c
Console.WriteLine(Util.Sum(2, 4, 6, 8));
```

此语句调用了 `Sum` 方法并传递了四个 `int` 参数。此调用匹配了 `Sum` 方法的重载。

6. 在 调试 菜单上，点击 无带调试 以编译并运行应用程序。

当应用程序运行时，它显示以下消息：

Using optional parameters

20

在这种情况下，编译器生成的代码调用了接收四个可选参数的方法。这是与方法调用最匹配的方法版本。

7. 按回车键返回 Visual Studio。
8. 在 `doWork` 方法中更改调用 `Sum` 方法的语句并移除最后一个参数 (8)，如下所示：

点击此处查看代码图像

```c
Console.WriteLine(Util.Sum(2, 4, 6));
```

9. 在 调试 菜单上，点击 无带调试 以编译并运行应用程序。

当应用程序运行时，它显示以下消息：

点击此处查看代码图像

Using optional parameters

12

即使方法签名并不完全匹配，编译器仍然生成了调用接收可选参数方法的代码。在接收可选参数的方法和接收参数列表的方法之间进行选择时，C# 编译器将使用接收可选参数的方法。

+ 10. 按回车键返回 Visual Studio。
+ 11. 在 `doWork` 方法中更改调用 `Sum` 方法的语句并增加两个参数：

点击此处查看代码图像

```c
Console.WriteLine(Util.Sum(2, 4, 6, 8, 10));
```

+ 12. 在 调试 菜单上，点击 无带调试 以编译并运行应用程序。

当应用程序运行时，它显示以下消息：

点击此处查看代码图像

Using optional parameters

30

这一次，提供的参数比可选参数指定的更多，编译器调用了接收可选参数的方法。

+ 13. 按回车键返回 Visual Studio。

### 总结

在本章中，你学习了如何使用 `params` 数组来定义接收任意数量参数的方法。你还学习了如何使用对象类型的 `params` 数组来创建接收任意类型参数的方法。你还了解了在参数数组方法和可选参数方法之间进行选择时，编译器是如何解析的。

- 如果你想继续后续章节，请保持 Visual Studio 2017 运行并转到第 12 章“处理继承”。
- 如果你现在想退出 Visual Studio 2017，请在文件菜单上点击退出。如果出现保存对话框，请点击“是”。

### 快速参考

|  | 执行操作 |
| --- | --- |
| 编写一个接收任意数量类型参数的方法 | 编写一个参数为给定类型 `params` 数组的方法。例如，一个接收任意数量 `bool` 参数的方法声明如下：<br>[点击此处查看代码图像]<br>```c\nType Method(params bool[] flags)\n{\n  ..\n}``` |
| 编写一个接收任意类型参数的方法 | 编写一个参数为 `object` 类型 `params` 数组的方法。例如：<br>[点击此处查看代码图像]<br>```c\nType Method(params object[] paramList)\n{\n  ..\n}``` |

## 处理继承

完成本章后，你将能够：

- 创建自基基类的派生类。
- 使用 `new`、`virtual` 和 `override` 关键字控制方法的隐藏和重写。
- 使用 `protected` 关键字限制继承层次结构中的访问权限。
- 定义扩展方法以作为使用继承的替代机制。

继承是面向对象编程世界中的一个核心概念。你可以将继承作为工具，在定义具有共同特征且有明确关联的类类时避免重复。也许它们是同种类型的不同类，例如工厂的 *经理*、*体力工人*以及*所有员工*。如果你正在编写一个模拟工厂的应用程序，你该如何指定经理和体力工人既有相同特征又有不同特征呢？例如，他们都有员工编号，但经理承担的职责和执行的任务与体力工人不同。

这就是继承大显用场的地方。

# 什么是继承？

如果你向几位经验丰富的程序员询问“继承”一词的含义，你通常会得到不同且冲突的答案。这种困惑部分源于“继承”这个词本身有几个细微的含义。如果有人在遗嘱中将某物留给你，你就被认为继承了它。同样，我们说你从母亲那里继承了一半基因，从父亲那里继承了另一半基因。这两个词的这些用法与编程中的继承几乎没有关系。

编程中的继承完全在于分类——它是类与类之间的关系。例如，当你上学时，你可能学习过哺乳动物的知识，并学习了马和鲸鱼是哺乳动物的例子。每种动物都拥有哺乳动物的所有属性（呼吸空气、哺乳养幼崽、温血动物等），但每个动物也有它们自己的特殊特征（马有蹄子，而鲸鱼有鳍和尾鳍）。

你如何在程序中为马和鲸鱼建模？一种方法是创建名为 `Horse` 和 `Whale` 的不同类。每个类都可以以自己的方式实现该类型哺乳动物特有的行为，例如马的 `Trot`（（小跑）或鲸鱼的 `Swim`（游泳）。但你如何处理马和鲸鱼共有的行为，如 `Breathe`（呼吸）或 `Suckle`（哺乳）？你可以在两个类中添加这些名称的重复方法，但这种情况会变成维护的噩梦，特别是当你还决定开始建模其他类型的哺乳动物，如 `Human`（人类）和 `Aardvark`（土蚁）。

在 C# 中，你可以使用类继承来解决这些问题。马、鲸鱼、人类和土蚁都是哺乳动物，因此你可以创建一个名为 `Mammal` 的类，提供这些类型展示的共同功能。然后你可以声明 `Horse`、`Whale`、`Human` 和 `Aardvark` 类都继承自 `Mammal`。这些类自动包含了 `Mammal` 类的功能（`Breathe`、`SuckleYoung` 等），但你也可以为每个类增加特定哺乳动物特有的功能——`Horse` 类的 `Trot` 方法和 `Whale` 类的 `Swim` 方法。如果你需要修改 `Breathe` 等公共方法的工作方式，你只需要在一个地方进行更改，即 `Mammal` 类。

### 使用继承

你通过以下语法声明一个类继承另一个类：

点击此处查看代码图片

```
class DerivedClass : BaseClass
{
}
```

派生类继承自基类，基类中的方法成为派生类的一部分。在 C# 中，一个类最多允许派自一个基类；类不允许派自两个或多个类。然而，除非 `DerivedClass` 被声明为 `sealed`（密封的），否则你可以使用相同的语法派生自 `DerivedClass` 的派生类。（你将在第 13 章“创建接口和定义抽象类”中学习密封类。）

点击此处查看代码图片

```
class DerivedSubClass : DerivedClass
{
}
```

继续前述描述的示例，你可以如下声明 `Mammal` 类。`Breathe` 和 `SuckleYoung` 方法是所有哺乳动物共有的。

点击此处查看代码图片

```
class Mammal
{
    public void Breathe()
    {
    }

    public void SuckleYoung()
    {
    }
}
```

然后你可以为每种不同类型的哺乳动物定义类，根据需要添加更多方法，如下例所示：

点击此处查看代码图片

```class
class Horse : Mammal
{
    public void Trot()
    {
    }
}

class Whale : Mammal
{
    public void Swim()
    {
    }
}
```

注意：如果你是 C++ 程序员，你应该注意到你不需要显式地指定继承是公有的、私有的还是保护的。C# 继承始终是隐式公共。如果你熟悉 Java，请注意冒号的使用，以及没有 `extends` 关键字。

如果你在应用程序中创建一个 `Horse` 对象，你可以调用 `Trot`、`Breathe` 和 `SuckleYoung` 方法：

点击此处查看代码图片

```cs
Horse myHorse = new Horse();
myHorse.Trot();
myHorse.Breathe();
myHorse.SuckleYoung();
```

同样，你可以创建一个 `Whale` 对象，但这次你可以调用 `Swim`、`Breathe` 和 `SuckleYoung` 方法；`Trot` 方法是不可用的，因为它只在 `Horse` 类中定义。

> **重要** 继承仅适用于类，不适用于结构体（structures）。你不能用结构体定义自己的继承层次结构，也不能定义派自类或另一个结构体的结构体。

所有结构体实际上继承自一个名为 `System.ValueType` 的抽象类。（第 13 章探讨了抽象类。）这完全是 Microsoft .NET Framework 定义基于栈的值类型的共同行为的实现细节；你不太会在自己的应用程序中直接使用 `ValueType`。

## 重新回顾 System.Object 类

`System.Object` 类是所有类的根。所有类都隐式派自 `System.Object`。因此，C# 编译器静默地将 `Mammal` 类重写为以下代码（如果你真的想，也可以显式地写）：

点击此处查看代码图片

```cs
class Mammal : System.Object
{
}
```

`System.Object` 类中的任何方法都会通过继承链传递给派自 `Mammal` 的类，例如 `Horse` 和 `Whale`。在实践，这意味着你定义的所有类都自动继承 `System.Object` 类的所有特征。这包括如 `ToString` 等方法（在第 2 章“使用……”中讨论）。

## 调用基类构造函数

除了继承的方法外，派生类还自动包含基类的所有字段。记住，所有类都至少有一个构造函数。（如果你没有写任何非默认构造函数，编译器会为你生成一个默认构造函数。）

派生类中的构造函数调用基类构造函数以指定任何额外的初始化是一个良好的做法，例如所示：

```cs
class Mammal // 基类
{
    public Mammal(string name)
    {
    }
}

class Horse : Mammal // 派生类
{
    public Horse(string name) : base(name)
    {
    }
}
```

如果在派生类构造函数中没有显式调用基类构造函数，编译器会尝试静默地插入对基类默认构造函数的调用。以上以上示例，编译器会将：

```cs
class Horse : Mammal
{
    public Horse()
    {
    }
}
```

重写为：

```cs
class Horse : Mammal
{
    public Horse() : base()
    {
    }
}
```
