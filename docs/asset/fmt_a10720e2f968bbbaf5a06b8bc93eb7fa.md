
```csharp
// 使用此进行初始化
void Start ()
{
    System.IO.Stream;
    System.IO.FileStream;
    System.IO.MemoryStream;
    System.IO.StreamReader;
    System.IO.StreamWriter;
    System.IO.UnmanagedMemoryStream;
}
```

通过这个技巧，我们将使用 `StreamWriter` 创建一个文本文件。

```csharp
void Start ()
{
    StreamWriter writer = new StreamWriter("myfile.txt");
    writer.WriteLine("hello");
}
```

使用 `StreamWriter` 创建了一个名为 `writer` 的对象。在 `StreamWriter` 实例化时，我们传递了一个字符串作为文件名。在我们自己的库中，我们将能够编写实用的函数，这些函数可以像 `UnityEngine` 中的任何内容一样被使用。在 `File.txt` 中，我们通过 `writer` 调用 `WriteLine` 写入一些内容。之后，我们需要调用 `Flush()` 来完成操作。

# 基础：代码的构建模块

将脚本挂载到场景中的主相机（Main Camera）上，并在 Project 视图中查看 `Start()` 函数。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_0.png)

在 `File.txt` 中，我们可以看到写入的内容。

| 属性 | 属性 |
| :--- | :--- |
| 创建 | 2023-10-27 |
| 大小 | 1 KB |

---

# 使用 Unity 3D 学习 C# 编程

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_0.png)

在 Mono 中，展开解决方案管理器中的 References（引用）图标。如果解决方案面板没有打开，请使用以下菜单显示面板：View（视图）→ Solution（解决方案）。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_1.png)

双击 References 文件夹下的 `Unity.dll`。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_2.png)

程序集浏览器程序将打开，并向你展示你可以访问的各种库。在 `FirstExample.cs` 类中，输入关键字 `key` 将会弹出一个窗口。该弹出窗口将向你提示 Unity 3D 提供了可用的许多不同的库。

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

随后，你将看到可以添加到项目中的各种库的提示。通过添加 `using`，我们可以访问以前在没有指令的情况下无法使用的新函数。

```csharp
// 使用此进行初始化
void Start () {
    /*
    TreeEditor vs TreeInstance {
    TreePrototype
    } */
}
```

我们不会深入探讨如何使用这些其他函数。我们现在只是在了解已经拥有的函数。在 `UnityEngine` 和 `System.Collections` 之间，我们已经准备好了一套工具工具。以后，我们将能够创建自己的库。在我们自己的库中，我们将能够编写实用的函数，这些函数可以像 `UnityEngine` 中的任何内容一样被使用。

在我们的 `FirstExample.cs` 中，我们将使用 `Start()` 函数并寻找 `StreamWriter` 函数。

```csharp
// 使用此进行初始化
void Start () {
    StreamWriter writer = new StreamWriter();
}
}
```

然而，当我们开始输入正在寻找的函数时，自动补全窗口显示“未找到完成项”（No Completions Found）。我们应该使用长路径版本，这样就能看到它隐藏在 `System` 中。在 `System.IO` 内部，我们发现了几个包含 `Stream` 的对象。

```csharp
// 使用此进行初始isation
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

但是，如果我们添加了 `using System.IO;` 指令，我们就可以缩短代码。`using` 关键字帮助我们建立库中的类与我们代码之间的链接。我们对正在使用的对象越明确，在添加指令后需要编写的代码就越少。

```csharp
// 使用此进行初始化
void Start ()
{
    System.IO.Stream;
    System.IO.FileStream;
    System.IO.MemoryStream;
    System.IO.StreamReader;
    System.IO.StreamWriter;
    System.IO.UnmanagedMemoryStream;
}
```

通过这个技巧，我们将使用 `StreamWriter` 创建一个文本文件。

```csharp
void Start ()
{
    StreamWriter writer = new StreamWriter("myfile.txt");
    writer.WriteLine("hello");
}
```

使用 `StreamWriter` 创建了一个名为 `writer` 的对象。在 `StreamWriter` 实例化时，我们传递了一个字符串作为文件名。在我们自己的库中，我们将能够编写实用的函数，这些函数可以像 `UnityEngine` 中的任何内容一样被使用。在 `File.txt` 中，我们通过 `writer` 调用 `WriteLine` 写入一些内容。之后，我们需要调用 `Flush()` 来完成操作。

# 基础：代码的构建模块

将脚本挂载到场景中的主相机（Main Camera）上，并在 Project 视图中查看 `Start()` 函数。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_125_0.png)

在 `File.txt` 中，我们可以看到写入的内容。

| 属性 | 属性 |
| :--- | :--- |
| 创建 | 2023-10-27 |
| 大小 | 1 KB |

现在我们可以为 Unity 3D 编写函数了，让我们开始真正的编码吧。为了创建所有这些变量，我们需要函数。函数包含了每种情况下的逻辑。这个概念在大多数面向对象的编程语言中都是相同的。

注意：函数在不同的编程语言中看起来可能不同，但它们的工作方式大多是相同的。通常的模式是使用数据并用逻辑处理这些数据。函数也可以有其他名称，例如方法（methods）。

主要区别在于不同语言使用的方式不同。语法基本上是空格或制表符、运算符或关键字的使用。归根结底，你所做的只是告诉编译器如何将你的函数转换为计算机解释的命令。

变量和函数构成了编程的大部分。任何你想记住的数据都存储在变量中。变量由你的函数管理。通常情况下，当你将变量和函数放在一起时，你就称它为一个类（class）。

在第 3 章中，我们讨论了如何编写一个类，其中声明以及开头和结束的大括号 `{}` 构成了主体。函数的编写方式类似。

我们从声明 `void myFunction();` 开始，然后添加括号 `()` 和大括号 `{}`，这告诉我们自己可能填充或不填充这些内容。第一对括号 `()` 并不要求添加任何内容。然而，大括号 `{}`（即函数的体）确实需要添加代码以使函数具有任何意义。

在编写新函数时，在继续另一个任务之前，填充整个函数的布局是一个良好的习惯。这会让编译器感到轻松；如果将一个函数留在 `void myFunction` 的形式并转向另一个任务，会让编译器困惑于你打算做什么。

集成开发环境（我们称之为 MonoDev）会不断读取和解释你正在编写的内容，就像文字处理器中的拼写检查器一样。当它遇到没有结论的语句（例如变量、函数或类定义）时，它对你编写代码的解释将引发警告或错误。MonoDev 看起来可能有点挑剔，但它正在尽力提供帮助。

## 4.6.2 3D 实体点

3D 开发者为我们提供的 `MonoBehaviour` 是一个类，允许我们的 C# 类访问 Unity 3D 游戏引擎的内部机制。`MonoBehaviour` 类是 Unity 3D 特有的函数和数据类型的集合。我们将在后面的教程中学习如何使用这些 Unity 3D 的函数。

注意：同样重要的是，在学习 Unity 3D 的细节时，你应该意识到 Unity 3D 特定的课程可以应用于其他开发。当你在 Windows 或 OS X 上使用 C# 时，你将能够为 Unity 3D 以外的其他操作系统编写应用程序。

将 `MonoBehaviour` 想象一组与 Unity 3D 通信的工具。其他系统有不同的工具集来制作应用程序。在读完这本书并学习如何与 Unity 3D 通信之后，学习如何使用其他系统将会得多。

在处理应用程序时，你需要使用 `Main()` 作为 C# 程序的起点。这类似于许多其他环境，如 C++ 和 C。

当类添加 Unity 3D 创建基础时，Unity 3D 会自动添加 `void Start()` 和 `Update()`。这两个函数是入口点。基本上，基类 `MonoBehaviour` 有几个函数，包括 `Start()` 和 `Update()`，这些函数基于游戏运行时发生的事件。

还有其他函数在运行 `MonoBehaviour` 时也会被自动调用：`Awake()`、`OnEnable()`、`Update()`、`FixedUpdate()` 和 `LateUpdate()`；这些函数通常在对象创建且你的游戏运行时被调用。当对象被销毁时，会调用 `OnDestroy()`。还有可以被调用的渲染函数，但我们不需要在这里讨论。

为了理解游戏每帧期间发生了什么，最好的方法是将游戏想象成电影运行。在游戏的最开始，当玩家开始时，场景中每个带有 `MonoBehaviour` 脚本的演员都会被调用 `Start()` 方法。

调用函数基本上是执行位于函数声明之后的大括号内部的代码行。在第一帧结束之前，场景中每个脚本的 `Update()` 函数会以无特定顺序被调用。

在下一帧开始时，如果场景中有新的脚本，`Start()` 函数将不会被调用。如果只向场景引入了新脚本，`Start()` 函数会在新场景中被调用。如果 `Start()` 中没有代码，或者脚本中没有 `Start()` 函数，则什么都不会发生。

为了从每帧发生的任何事情中获益，你需要将代码放入 `Update()` 函数中。当一个类首次引入游戏世界时，你需要将代码添加到 `Start()` 函数中。你可以根据需要使用所有它们。重要的是，这些入口点将使你的类能够独立运行。

函数有特定的名称或标识符。因此在我们看过的 `Start()` 和 `Update()` 之后，我们在整本书中还将使用许多函数。我们将使用的第一个函数是 `Log()`，它是在 `Debug` 类内部找到的函数。我们稍后会回到如何使用这个函数，但我们将演示它是如何工作的。

如果 `Debug` 是一个类，那么 `Log()` 就是 `Debug` 的成员。点运算符允许我们访问在 `Debug` 类中找到 `Log()` 函数。

```csharp
void Start() {
    // 这将在 Unity 控制台中打印出 "start"
    Debug.Log("start");
}
```

# 基础知识：代码的构建块

```
void SimpleFunction () {
    Debug.Log("simple function is being called");
}
void Start () {
    SimpleFunction();
}
```

`SimpleFunction ()` 在类中的位置不会影响它的调用方式。为了方便说明，只要它在类作用域内已声明，我们可以在类的任何地方使用 `SimpleFunction ()`。

```
void Start () {
    SimpleFunction();
}
void SimpleFunction () {
    Debug.Log("simple function is being called");
}
```

我们在声明 `SimpleFunction()` 之前就使用了它。你可能注意到 `Debug.Log()` 看起来与我们的简单函数相似。标识符后跟着括号内的文本是一种常用的用法。

```int
int a = 0;
void SetAtThree () {
    a = 3;
}
void Start () {
    Debug.Log(a);
    SetAtThree();
    Debug.Log(a);
}
```

为了让函数工作，我们需要给它提供指令。如果我们声明一个 `int a` 并将其设置为 `0`，我们就有了一些初始数据。创建一个新函数 `SetAtThree()`，并在它的代码块中告诉它将 `a` 设置为 `3`。如果在 `Start ()` 函数中打印，得到的是 `0`，即初始设置的值。然后执行函数 `SetAtThree()`，它将 `a` 设置为 `3`，因此当再次打印时，它的新输出是 `3`。

| 项目 | 控制台 |
| :--- | :--- |
| Clear | Collapse | Clear on play | Error pause |
| 1 | UnityEngine.MonoBehaviour:print(Object) |
| 3 | UnityEngine.MonoBehaviour:print(Object) |

# 4.6.4 空格与制表符

制表符（Tabs）用于界定函数的内容。到目前为止，我们看到的每个函数内容都通过向右缩进了一个制表符。

# 使用 Unity 3D 学习 C# 编程

```c
void MyFunction()
{
    // 缩进一次
    int i = 0;
    // while 语句也缩进一次
    while (i < 10) {
        // while 语句的内容缩进两次
        print(i);
        i++;
    }
}
```

函数的内容缩进了两次，如箭头所示。这种表示方式有助于明确 `while` 语句内部的内容的执行方式与函数的其余部分不同。

为了帮助理解计算机是如何处理上一个代码片段的，我们将逐行分析代码。这模拟了函数在被调用时的运行过程。当然，计算机执行这些速度非常快，但要理解计算机正在以比我们理解能力快数百万甚至十亿倍的速度执行的操作是必要的。

```csharp
void MyFunction()
    // 缩进一次
    int i = 0;
    // while 语句也缩进一次
    while (i < 10) {
        // while 语句的内容缩进两次
        print(i);
        i++;
    }
```

注意：想象一下，你的中央处理器（CPU）是由每秒旋转超过 20 亿次的齿轮组成的。2.4 GHz 意味着每秒 2,400,000,000 个周期。一个周期是硅片中每个晶体管的更新：超过20 亿个电子脉冲流过硅片，每个脉冲根据你的指令开启或关闭各种晶体管。当然，并不是所有的周期都用于你的游戏；许多周期被 Unity 3D 操作系统占用，因此性能始终会有其限制。

第一行 `MyFunction()` 被计算机识别并用于定位要执行的代码。一旦函数启动，代码内容从第一条语句开始。在这种情况下，我们 `//` 缩进一次，这是一个注释，会被计算机忽略。

接下来是 `int i = 0;`，这是对名为 `i` 的变量的声明和赋值，`i` 是一个你熟悉的标识符，我们将使用 `i` 来定位该数据。

在变量声明之后，我们遇到了另一个被计算机忽略的注释。`while (i < 10)` 这行代码连接并为内存中的另一个空间用于某些操作。这还创建了与变量 `i` 的连接，以检查 `while` 语句是否执行。如果 `i` 的值小于 10，则将执行内容；否则，`while` 语句的内容将被忽略。

函数找到另一个字符——左大括号 `{`，这让它识别出一个新的执行上下文。计算机将读取并执行 `while` 语句中的每一行，直到找到右大括号 `}`。在这个新的上下文中，我们将返回第一个大括号，直到 `while` 语句的条件为假。

由于 `i` 小于 10，`while` 语句的条件为真，因此我们将执行 `while` 语句的第一行。在这种情况下，这是一个被忽略的注释。随后是一个 `print` 函数，
