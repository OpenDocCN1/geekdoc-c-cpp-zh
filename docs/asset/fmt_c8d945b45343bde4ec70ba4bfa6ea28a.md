
在 C# 类的顶部，我们必须使用 `#define` 创建一个新的指令。在这种情况下，我们 `#define TESTING` 来表示我们可能正在代码中测试特定内容。一旦定义了预处理器指令，它将用于类的其余部分。

向下看，我们在 `Start()` 函数中使用 `#if TESTING`，后面跟着 `Debug.Log("just testing");`，然后是 `#endif` 结束指令执行的语句。这段代码的结果允许我们轻松选择代码块来开启或关闭。

```
just testing
UnityEngine.Debug:Log(Object)
Preprocessor:Start () (at Assemblies/Preprocessor.cs:10)
normal behavior
UnityEngine.Debug:Log(Object)
Preprocessor:Start () (at Assemblies/Preprocessor.cs:12)
```

上面的代码中 `#define TESTING` 位于类顶部。这里变得更有趣了。如果我们注释掉 `#define TESTING` 并保持其他代码不变，我们得到的结果表现就像 `Debug.Log("just testing");` 并不存在。

你可能还会注意到，由于顶部的 `#define TESTING` 被注释掉，`#if TESTING` 和 `#endif` 之间的行也需要被注释掉！当代码运行时，测试日志不会发送到控制台，因为 `TESTING` 未被定义：当然，你可以

# 高级 505

同样检查此情况。如果我们让 `//#define TESTING` 保持注释状态，我们将获得测试代码工作，如果使用使用预处理器：

```csharp
#if TESTING
Debug.Log("just testing");
#endif
```

上面的 `#if TESTING`，或者说 "if testing." 现在会在控制台中再次显示。这样的预处理器可以根据是否定义 `TESTING` 来完全省略代码。

```text
1 //define TESTING
2 using UnityEngine;
3 using System.Collections;
4
5 public class Preprocessor : MonoBehaviour
6 {
7 //用于初始化
8 9 void Start()
10 {
11 #if TESTING
12 Debug.Log("just testing"); //
13 #endif
14 Debug.Log("normal behavior");
15 }
```

这就是为什么它被称为预处理器。根据指令的设置，你可以从不同的版本中省略整个代码段。值得注意的是，你必须在代码中任何标记出现之前放置所有的 `#define` 指令，因此所有 `#define` 语句必须出现在类的顶部。

使用 `#if` 预处理器是一种根据程序员添加或删除各种指令来管理执行代码的聪明方法。在 Unity 3D 中，我们获得一组非常有用的预定义指令。

## 7.11.2 UNITY_EDITOR

在 `Directives.cs` 文件中，查看 `#if UNITY_EDITOR` 所在的行。

```csharp
#if UNITY_EDITOR
Debug.Log("im an editor only message");
#endif
```

`UNITY_EDITOR` 只在编辑器运行时定义。符号定义的完整列表可以在 Unity 3D 网上找到。其他符号包括 Unity 3D 版本号和游戏运行的平台。

当游戏在独立模式或移动设备上运行时，`UNITY_EDITOR` 指令不存在，因此 `#if UNITY_EDITOR` 预处理器指令中的任何代码都将跳过编译。在编辑器中运行时，拥有特定的行为通常很有用。当你发现自己在编辑器中更改数字时，这可以提高速度。

```csharp
public int health = 10;
void Start () {
#if UNITY_EDITOR
health = 1000;
#}
```

通过这种方式，我们可以轻松跳过每次在编辑器中启动游戏时修改数字。这还能防止我们不小心勾选某些代码可能会影响游戏的最终发布。我们可以在指令的使用上增加一些复杂性。

```csharp
//define LOWHEALTH
using UnityEngine;
using System.Collections;
public class Directives : MonoBehaviour
{
    // 使用此代码进行初始化
    public int health = 10;
    void Start ()
    {
        #if UNITY_EDITOR && LOWHEALTH
        health = 1;
        #elif UNITY_EDITOR
        health = 1000;
        #endif
    }
}
```

在这里，我们可以注释或取消顶部的指令定义，并在低血量（`LowHealth`）和 Unity 编辑器测试之间切换。第一个预处理器 `#if UNITY_EDITOR && LOWHEALTH` 仅在我们编辑器中运行且取消了类开头处 `#define LOWHEALTH` 指令注释时才会设置。`&&` 运算符的工作原理与我们在 `if` 语句中使用的相同。

为了使更清晰，我们可以在预处理器条件 `#if (UNITY_EDITOR && LOWHEALTH)` 周加上括号，这会产生结果。这并不是强制要求的；然而，编程风格可能会决定你在任何地方使用它。要在两个语句之间切换，我们使用 `#elif`，它是你在代码其他部分通常使用的 `} else if {` 的预处理器版本。

这种差异源于一个源自旧版且集成程度较低的旧习惯。文本编辑软件实际上在编译之前会遍历每个文件并进行删除。每个 `#command` 必须是一个单词，宏才能正常工作。现在宏已经被整合到了解析器中，但格式还没有改变。我们看到的也是 `#endif` 而不是闭合括号或大括号。

这这是一套完全不同的语言，而且这也有其好处。它能更明显地表明代码之上正在发生第二组动作，而不是使用像下面这样的内容：

```csharp
void Start ()
{
    if (UNITY_EDITOR && LOWHEALTH)
    {
        health = 1;
    }
    else if (UNITY_EDITOR)
    {
        health = 1000;
    }
}
```

这些是否是指令并不那么清晰。真正的问题是，这些代码会被编译到发布版的游戏中，而且可能有人在检查之前不小心留了某个勾选框。当然，真正的问题是提交到游戏发布版本中的代码包含了本不需要存在于那里的额外代码。

## 高级

```csharp
public bool isEditor = false;
```

当然，我们实际上可以根据使用情况来开启或关闭这些复选框。然而，通过简单添加 `#if UNITY_EDITOR` 提供的自动化要简单且自动得多，而且不容易出错。

## 7.11.3 警告

在使用 `#define` 进行调试时，提醒自己要使用 `#undef` 来关闭任何已激活的指令是重要的。作为一种自我提醒，可以在 `#if` 之后添加 `#warning`，作为 Unity 3D 中的一个提醒，告知你的指令正在发生哪些修改。

```csharp
#define TESTING
using UnityEngine;
using System.Collections;
using System;
public class Directives : MonoBehaviour {
    // 使用此代码进行初始化
    void Start() {
        int playerHealth = 100;
#if TESTING
#warning DEBUG is on
playerHealth = 100000;
#endif

        if(playerHealth < 0) {
            Debug.Log("player died");
        }
    }
}
```

在将此添加到代码后，当脚本被 Unity 3D 解析时，你会得到一个“DEBUG is on”的警告。这段文字可以是你喜欢的任何内容，只要你给自己的警告是有意义的即可。警告消息没有特殊格式，因此在消息中间添加一行将破坏你的代码。

```csharp
#warning don't add a line
break in the middle of a warning
```

那样不会的。你的消息需要保持在出现 `#warning` 所在的行上。通用的规则是，这些应该用于其余 `#define` 预处理器指令。所有大写命名并不是强制的，尽管它是种常见的做法。这指出了你的代码中任何特殊情况定义是在何处发生的。

```csharp
#if TESTING
#warning DEBUG is on
playerHealth = 100000;
#elif UNITY_EDITOR
playerHealth = 100000;
#endif
```

预处理器指令中的 `else if` 等效项已缩短为 `#elif`，其工作方式与你预期的普通 `if-else` 语句相同。

## 7.11.4 组织

组织是一场持久的斗争。在 MonoDevelop 中，你有用于折叠代码的小框。`#region NAME` 是一个非常有用的指令，用于保持开发环境的洁。

# 508

# 使用 Unity 3D 学习 C# 编程

```csharp
public class Directives : MonoBehaviour
{
    #region IMPORTANTFUNC
    void ImportantFunc()
    {
        int j = 10;
        #region SPECIFICPART
        // 这里有很多内容
        int i = 0;
        while (i < 10)
        {
            // 更多内容
        }
        #endregion
        while (j --> 0)
        {
            // 更多内容
        }
    }
    #endregion
}
```

在上面的代码中，`#region` 可以嵌套。注意嵌套的区域。

![](img/5ac639a69dd6fbc68eba1d4ca9f7_529.png)

## 高级

这将帮助你跳转到 `#regions` 或 `#if`，尽管这里的危险是它们在使用之前可能已经被更改了。这些指令中的某些在日常编程中提供了最大的实用性。`#pragma` 是我们用来告诉编译器遵守哪些特殊函数的指令。

## 7.11.5 我们学到的知识

在我们涵盖了错误处理概念后，我们将再次回到一些预处理器指令上。通常情况下，预处理器处理代码的方式更接近注释的工作方式。正因如此，我们可以根据类开头的单个 `#define` 来管理不同的代码块。

指令用于许多不同的事情：最常见的用途之一是管理多平台的工作。使用预处理器指令，你可以根据平台或模型设置不同的配置。

## 7.12 异常

处理诸如未使用变量等少量警告是足够简单的；警告过多可能会导致重要的警告被忽略。通常情况下，最好将你的警告减少到最低，或者至少完全没有意外的警告。

在某些情况下，我们可能想要特定的警告。当我们尝试从网页读取统一资源定位符（URL）而服务器宕机时，我们的游戏不会直接崩溃或冻结。

某些情况下，我们可能期望某些值是错误的。在与用户交互时，你可能期望一个数值却得到了一个字母。与其冻结和崩溃游戏，你可以忽略输入直到进行纠正。

## 7.12.1 基础示例

在 Unity 3D 项目中，我们在场景中设置了如下 `Warnings.cs`，带有简单的 `Update()` 函数。在类作用域内，我们使用一个公共字符串，它将允许你输入任何字符串值。

```csharp
using UnityEngine;
using System.Collections;
public class Warnings : MonoBehaviour
{
    public string input;
    void Update ()
    {
        int i;
        try{
            i = int.Parse(input);
        }
        // 不，没用……
        catch{
            i = 0;
        }
        Debug.Log("i = " + i);
    }
}
```

这段代码允许我们在输入字段中使用任何字符串，这将导致错误。如果没有 `try-catch{}` 关键字，我们的 `Update ()` 函数看起来会如下所示：

```cs
void Update () {
    int i;
    i = int.Parse(input);
    Debug.Log("i = " + i);
}
```

由于字符串中使用了其他异常，我们将在控制台（Console）面板中看到大量的错误。

FormatException: 输入字符串格式不正确

System.Int32.Parse(System.String s) (at/Applications/buildAgent/b5b9ae78cff0584/mcs/class/corlib/Int32.cs:629)

Warnings.Update (at Assets/Warnings.cs:15)

`try{}` 语句用于对 `input = int.Parse(input)` 进行处理。如果执行失败，`catch{}` 会捕获该失败并进行修正。如果 `try{}` 执行成功，则不会调用 `catch{}`。如果初始解析成功，我们可以对 `try` 语句进行额外的修改。

我们可以通过传递到 `catch{}` 的某些参数，提供关于发生错误的更多详细信息。首先，我们将在类的开头添加一个新的指令。

```cs
using UnityEngine;
using System.Collections;
using System;
```

在指令中添加 `using System` 将允许我们的 `catch{}` 调用识别 `Exception` 类型。

```cs
catch (Exception e) {
    Debug.LogWarning(e);
    i = 0;
}
```

当输入任何无效内容时，我们会获得以下警告：

System.FormatException: 输入字符串格式不正确

这意味着我们不仅知道 `try{}` 失败了，还知道它为什么失败。我们可以对失败创建一个响应。当由于不同原因导致失败时，我们可以为每种情况创建不同的 `catch`。

## 7.12.2 异常消息 (Exception Messages)

`Exception` 类的重写方法之一是消息（message）。我们可以使用消息告诉我们什么创建了异常，以及我们可以如何处理它。

```cs
int CheckInput (string s) {
    int parsed = 0;
    if(string.IsNullOrEmpty(s)) {
        throw new Exception("null");
    }
    parsed = int.Parse(s);
    return parsed;
}
```

## 高级 (Advanced)

## 511

让我们从一个可以检查不同类型输入问题的新函数开始。通过上面的代码，我们从一个解析后的 `int` 开始，并将赋值给传入的字符串。如果 `if` 语句检查传入的字符串是否为空；如果是这种情况，我们使用 `throw` 关键字并创建一个新的 `Exception()`，并以 "null" 作为参数。在 `Update ()` 函数中，我们将代码添加到 `try{}` 语句中。

```cs
void Update () {
    int i;
    // 尝试解析一个字符串
    try {
        i = CheckIn(input);
    } catch (Exception e) {
        Debug.LogWarning(e);
        i = 1;
    }
    Debug.Log("" + i);
}
```

紧随 `CheckIn()` 函数之后的 `catch()` 语句将捕获在此之前创建的 `Exception()`。这看起来可能有点随意，但它是 C# 的一个有趣特性。我们看到一个新的 `Exception()` 对象正在被创建，而一个 `catch()` 语句在没有直接告诉它这么做的情况下获取了它。事实上，有大量的底层架构允许了这一点。

当运行代码且检查器（Inspector）面板的输入面板没有输入内容时，我们会在 Unity 3D 的控制台中输出以下警告。

System.Exception : null

这里的字符串是我们创建 `Exception` 时输入的字符串。由于我们能够捕获这个问题并决定如何处理它，我们保护了游戏免受执行错误的影响。这里已经预定义了一些异常，用于在 `null` 成为问题时返回。

```cs
int CheckIn(string s)
{
    int parsed = 0;
    if(string.IsNullOrEmpty(s)) {
        throw new ArgumentException("please enter something");
        // 抛出了不同的异常！
    }
    parsed = int.Parse(s);
    return parsed;
}
```

我们可以通过一个寻找该抛出异常的 `catch` 来捕获此异常。一旦我们开始考虑继续操作之前需要输入某些数字的情况，这就会变得更加重要。
