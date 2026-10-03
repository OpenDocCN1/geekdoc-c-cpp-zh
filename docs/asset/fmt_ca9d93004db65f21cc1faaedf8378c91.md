
只有游戏观众中一小部分精通技术的群体才会注意到，例如玻璃是如何以真实的方式破碎的，或者角色在转身时脚部是如何着地的。许多开发者认为自己在游戏写实性上突破了，但对他们的玩家来说，他们花费了数千小时却没有让游戏变得更有趣。

## 基础：代码的构建模块

输入管理是我们的首要目标。你应该决定是处理键盘鼠标，还是触摸屏点击和手势。开发一个良好的输入管理系统需要时间和精力。这种投入通常贯穿整个项目。不断的调整和更新在游戏性和输入之间循环。

在第 3 章中，我们在场景中添加了一个立方体，并为其挂载了`Example.cs`脚本。这实际上足以构建一个沙盒。根据你的游戏，你可能想要添加地板和墙壁。这可以通过添加一些立方体并拉伸它们来构建一个可以行走的室内房间。

## 4.4 创建类

类是构建对象的指令集。这之前提到过，开始吧。

```c
关键字 标识符
class MyClass
{
    // 代码写在这里...
}
```

### 4.4.1.1 基础示例

C# 允许我们在类内部创建类。上面显示的是`VeryFirstClass`的类声明。这是`Example`类内部的一个嵌套类。为了演示用法，我们将使用新示例来构建一个`VeryFirstClass`对象。类的声明看起来像`class VeryFirstClass {}`，它创建了一个没有成员的新类。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_116_0.png)

紧接着下方，你会发现有一行包含`void Start ()`语句；此语句创建了一个作为`Example`类成员的函数。要创建该类的实例，我们在`Start()`函数中添加了`VeryFirstClass FirstClass = new VeryFirstClass ();`。

| 类型 | 赋值运算符 | 构造函数 | 分隔符 |
| --- | --- | --- | --- |
| `VeryFirstClass` | `FirstClass` | `= new VeryFirstClass ( ) ;` | |
| | 标识符 | 关键字 | 参数 |

让我们检查前两个单词（或标记）。第一个标记`VeryFirstClass`表示我们打算创建的对象类型。我们创建的类现在变成了一种数据类型。一旦`VeryFirstClass`被声明为一个类，它就成为了创建一个新对象的指令，该对象可以通过其标识符找到。

我们知道变量是由关键字后跟标识符声明的，例如`i;`；类变量的声明方式类似：`VeryFirstClass FirstClass`。然而，与`int`不同，类不能被直接赋值。

`int`与类之间的区别在于类型是如何创建并赋值的。我们将在对数据类型有更深入的理解后对此进行详细讨论，但目前我们必须将`int`视为一种基本类型。

### 4.4.1.2 值类型和引用类型

尽管我们声明了`VeryFirstClass`，但还没有让它执行任何操作。目前，`VeryFirstClass`中什么都没有。一旦我们开始向`VeryFirstClass`添加功能，给类赋值的操作就会变得模棱两可。在上下文中：

```
VeryFirstClass FirstClass = 1;// 这应该做什么？
```

如果`VeryFirstClass`是一个僵尸，那么`1`代表什么？是他的名字、他拥有的积分，还是他的护甲分值？因为 C# 无法确定，计算机也没有希望做出猜测。

这区分了像`int`这样的值类型和像`Class`这样的引用类型。然而，在进入关于类型的章节之前，我们需要了解更多关于类的知识，因此我们将回到开头。

因此，在创建引用类型的新实例时，我们需要使用`newClass();`的形式来为`SomeClass`类型的变量赋值。因此，`MyClass myClass = new MyClass();`用于为`MyClass`创建一个变量，并为变量`MyClass`分配正确类的新实例。为了清楚起见，`int`也可以用完全相同的方式分配`myClass`。

```
int i = new System.Int32();
```

如果我们想让`int`的声明看起来和类的声明完全一样，可以使用上面的语句。这种做法是不合寻常且没有必要的，但知道此类事物的存在是重要的，而且 C# 足够灵活，允许我们这样做。

### 4.4.2 添加数据字段

数据字段是类内部的任何类型的信息。我们将在第 6.5.3 节介绍数据类型的真正含义，但目前我们假设数据可以是任何内容，包括数字。当向类中添加数据字段时，我们实际上是为该类提供一个存储信息的地方，并允许类记住、存储或处理某些数据。例如，如果我们为游戏编写一个僵尸，我们需要僵尸来存储它有多少个大脑，或者它从玩家那里承受了多少次击。

```
VeryFirstClass
{
    int num;
}
```

要向`VeryFirstClass`添加数据字段，我们使用与声明任何其他变量相同的声明。这应该是显而易见的，但由于我们是在类内部编写类，这可能会有点令人困惑。然而，当它声明为`int num;`时，我们是不允许直接使用它的。

### 4.4.3 访问修饰符和点运算符

为了与类的成员交互，我们使用点运算符`.`来告诉 C# 我们想要访问类的成员。当向类中添加新的数据字段时，它会被分配一个类型和一个标识符。该标识符就变成了我们在点号之后用于访问该数据或函数使用的单词。

## 基础：代码的构建块

```
void Start () {
    VeryFirstClass FirstClass = new VeryFirstClass (
}
FirstClass::{
    M Equals public virtual bool
    Equals (
        object obj
    )
}
void Update () {
    M GetHashCode
    M GetType
    M ToString Summary
确定指定的 Object 是否等于当前
Object。
}}
```

如果在使用 MonoDevelop 时需要找到`num`数据字段，我们将在成员列表中看不到`num`数据字段。为了让`int num`可访问，我们需要`public`关键字。`public`关键字与其它几个改变类中变量可访问性的关键字类似；此类关键字被称为修饰符。我们将来会遇到几种访问修饰符，但目前我们只需要熟悉`public`访问修饰符。

```c
class VeryFirstClass {
    public int num;
}
```

## 基础：代码的构建模块

```csharp
{
  Debug.Log(OtherNum);
}
```

通过上面的示例，我们可以看到`OtherNum`并没有与`num`分组，而是它的声明写在打印它的函数之前。类数据字段在何处以及何时声明，并不会影响函数是否能看到它。事实上，声明语句的位置可以出现在类的底部，如下：

```csharp
class MyClass {
  public void PrintNum() {
    Debug.Log(num);
  }
  public void PrintOtherNum() {
    Debug.Log(OtherNum);
    // 声明在末尾。
    public int OtherNum;
    public int num;
  }
}
```

类的函数和数据成员可以以任何顺序出现。这一特性似乎违背了直觉。C# 代码完全符合规范且运行正常，忽略了不同成员的排列顺序。这一规则并不成立，特别是当我们涉及到代码的执行方式时，但在类级别，或者用程序员常说的类作用域来说，顺序是不重要的。

并不是所有的编程语言都允许这样做。例如，UnrealScript 强制所有变量必须位于函数的开头。在任何地方声明它们都会引发错误。C# 理解格式比清晰度更重要。将变量声明在它们使用的附近对于可读性非常重要。

### 4.4.5 类成员

当我们向类中添加函数和变量时，我们就是在向类中添加成员。在之前的示例中，`num`是`MyClass`的一个成员。`PrintNum()`以及类中包含任何其他函数或变量也是。我们可以将成员标记为`public`（公共），这意味着其他类可以访问它们，而不可访问的成员是`private`（私有）。

在大多数情况下，如果没有使用`public`，你就可以假设该成员属于`private`。私有成员无法从类外部访问，至少不能直接访问。然而，类内部或对该类的函数可以自由地修改它们。

### 4.4.6 我们学到了什么

我们涵盖了构成类的一些非常基础的概念。还有许多其他关键字和复杂的概念我们尚未触及。之后，我们将学习一些允许这些实现的巧妙技巧。

为了自己练习，你应该尝试创建不同的数据字段并向你的类中添加更多函数，以感受它们是如何工作的。当你学会使用更多关键字时，你应该将它们添加到类中，以检查你是否理解了这些关键字的工作原理。

`Example.cs`是一个类。在本章中，我们将`MyClass`创建为`Example`类内部的类。`MyClass`是嵌套类的示例，即类内部的类。你允许编写多个嵌套类。

```csharp
using UnityEngine;
using System.Collections;
public class Example : MonoBehaviour
{

class VeryFirstClass
{
    public int num = 0;
    public void PrintNum()
    {
        Debug.Log(num);
    }
}
class AnotherClass
{
    public int anotherNum = 1;
    public void PrintNum()
    {
        Debug.Log(anotherNum);
    }
}

// 使用此进行初始化
void Start ()
{
}
// Update 每帧被调用一次
void Update ()
{
}

```

我们可以在任何其他类中添加任意数量的类。嵌套类内部还可以包含更多的类。

```csharp
class AnotherClass
{
    public class InsideAgain
    {
        public int insideNum = 0;
        public void PrintInside()
        {
            Debug.Log(insideNum);
        }
        public int anotherNum = 0;
        public void PrintNum()
        {
            Debug.Log(anotherNum);
        }
    }
}
```

如果需要，可以将`InsideAgain`类添加到`AnotherClass`中。只要类是`public`的，我们就可以在类外部使用它们。

```csharp
void Start ()
{
    AnotherClass.InsideAgain ACIA = new AnotherClass.InsideAgain();
}
```

## 基础：代码的构建模块

```csharp
ACIA.insideNum = 10;
ACIA.PrintInside ();
}
```

使用来自`AnotherClass`的运算符，我们可以访问它内部的类。这种“类中类”的布局并不常见，但并没有什么阻止你这样做。重要的是要保持尽可能的简单。每增加一层模糊性，你就会增加一层复杂度。

点运算符（`.`）允许我们访问类的内容，包括类中的类。这种行为通过 C# 使用，并且所有的特性都依赖于类和类成员。我们将在第 5 章查看如何访问我们可以使用的许多函数。

我们一直都在嵌套类中工作。为了展示这在另一个类中如何工作，我们可以回到 Unity 3D 为`Example.cs`创建一个名为`AnotherExample.cs`的新类。如果我们打开`Example.cs`，就可以访问`AnotherExample`类。

```csharp
using UnityEngine;
using System.Collections;
public class AnotherExample : MonoBehaviour {
    // 使用此进行初始化
    void Start () {
}
    // Update 每帧被调用一次
    void Update () {
}
```

上面的类是由 Unity 3D 自动生成的。这意味着我们在`Example.cs`的`Start()`函数中可以像使用任何其他公共类一样使用该类。这意味着在原始`Example.cs`文件旁边有一个完全新的 C# 文件。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_122_0.png)

当我们在`Example.cs`类中编写代码时，可以从类内部访问`AnotherExample`类。

## 在 Unity 中学习 C#

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_123_0.png)

```csharp
void Start ()
{
AnotherExample aClass = new AnotherExample();
```

`Example.cs`中的`Start()`语句将创建一个`AnotherExample`类的实例。类在整个 Unity 3D 项目中都是可见的。这允许对象和类之间发送消息。只要它们被创建，它们就可以相互通信。

# 使用 Unity 3D 学习 C# 编程

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_0.png)

在 Mono 中，展开解决方案管理器（Solution explorer）中的 References（引用）图标。如果解决方案面板没有打开，请使用以下菜单显示面板：View（视图）→ Solution（解决方案）。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_1.png)

双击 References 文件夹下的 Unity.dll。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_2.png)

程序集浏览器程序（Assembly Browser）将打开，并向你展示你可以访问的各种库。在 FirstExample.cs 类中，输入关键字`key`将会弹出一个窗口。该弹出窗口将向你提示 Unity 3D 提供了可用的许多不同的库。

# 基础：代码的构建模块

```csharp
using UnityEngine;
using System.Collections;
using System;

public class AOT
{
    class Microsoft
    {
        class TreeEditor
        {
            class UnityEditor
            {
                class UnityEditorInternal {}
            }
        }
    }
}
```

随后，你将看到可以添加到项目中的各种库的提示。通过添加`using`，我们可以访问以前在没有指令的情况下无法使用的新函数。

```csharp
// 使用此进行初始化
void Start () {
    /*
    TreeEditor vs TreeInstance {
    TreePrototype
    } */
}
```

我们不会深入探讨如何使用这些其他函数。我们现在只是在了解已经拥有的函数。在`UnityEngine`和`System.Collections`之间，我们已经准备好了一套相当工具。以后，我们将能够创建自己的库。在我们自己的库中，我们将能够编写许多函数，这些函数可以像`UnityEngine`中的任何内容一样被使用。

在我们的 FirstExample.cs 中，我们将使用`Start()`函数并寻找`StreamWriter`函数。

```csharp
// 使用此进行初始化
void Start () {
    StreamWriter writer = new StreamWriter();
}
}
```

然而，当我们开始输入正在寻找的函数时，自动补全窗口显示“未找到完成项”（No Completions Found）。我们应该使用长路径版本，这样就能看到它隐藏在`System`中。在`System.IO`内部，我们发现了几个包含`Stream`的对象。

```csharp
// 使用此进行初始化
void Start ()
{
    System.IO.Stream;
    System.IO.EndOfStreamException;
    System.IO.FileStream;
    System.IO.MemoryStream;
    System.IO.StreamReader;
    System.IO.StreamWriter;
}
// Update
void Update ()
{}

public class StreamWriter
{
    /// <summary>
    /// 实现了一个 StreamWriter 用于按特定编码向流写入字符。
    /// </summary>
}
```

但是，如果我们添加了`using System.IO;`指令，我们就可以缩短代码。`using`关键字帮助我们建立库中的类与我们代码之间的链接。我们对正在使用的对象越明确，在添加指令后需要编写的代码就越少。
