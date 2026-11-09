
![](img/9862a98a1a2d3bb14334137965a1ec60_461_0.png)

图C#-7.27

出现一个消息框，显示所引发异常的详细信息（图C#-7.28）。

- 14. *单击* **确定** 按钮关闭消息框，如图C#-7.28所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_461_1.png)

图C#-7.28

现在我们来了解用户定义异常类。

## 使用用户定义异常类

除了使用预定义异常类之外，您还可以创建自己的异常类来处理异常。这类异常类称为**用户定义异常类**。由用户定义异常类处理的异常称为**用户定义异常**。需要注意的是，用户定义异常类派生自 **ApplicationException** 类。使用用户定义异常类的优点是可以以编程方式区分错误条件。

我们通过执行以下步骤创建一个应用程序，以了解用户定义异常类的用法：

- 1. *启动* **Visual Studio 2010**。
- 2. 从菜单栏*选择* **文件→新建→项目**。将打开**新建项目**对话框。
- 3. 在**新建项目**对话框左窗格的**已安装的模板**部分中，*选择* **Visual C#→Windows**。
- 4. 在右窗格中*选择* **控制台应用程序**以创建控制台应用程序。
- 5. 在**名称**文本框中*输入*应用程序名称 **UserExceptionClassExample**（该示例也可在随书光盘中找到），并在**位置**框中为应用程序输入适当位置。
- 6. *单击* **确定** 按钮关闭**新建项目**对话框。**UserExceptionClassExample** 应用程序即创建完成，如图C#-7.29所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_462_0.png)

图C#-7.29

- 7. 在代码编辑器中添加清单 7.9 给出的代码片段。

清单 7.9：展示创建和使用用户定义异常类的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace userExceptionClassExample
{
    class Program
    {
        static void Main(string[] args)
        {
            float x = -1.0F;
            try
            {
                if (x < 0)
                {
                    throw new MyException("Its a negative number");
                }
            }
            catch (MyException ex)
            {
                Console.WriteLine("Exception caught");
                Console.WriteLine(ex.Message);
            }
            finally
            {
                Console.WriteLine("Control entered in the finally block");
                Console.Read();
            }
        }
    }
    class MyException : ApplicationException
    {
        public MyException()
        {
        }
        public MyException(string message): base(message)
        {
        }
        public MyException(string message, ApplicationException ax):
        base(message, ax)
        {
        }
    }
}
```

在清单 7.9 中，我们创建了一个名为 **MyException** 的新异常类，它派生自 **ApplicationException** 类。在 **MyException** 类中，实现了基类的三个构造函数。在 **Main** 函数内部，我们声明了一个 float 类型变量 **x**，并为其赋了一个负值。这会引发 **MyException** 异常，控制流将转移到 **catch** 和 **finally** 语句。

- 8. 按 **F5** 键执行应用程序。输出如图C#-7.30所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_463_0.png)

图C#-7.30

如**图C#-7.30**所示，**x** 变量中的值为负数；因此会引发 **MyException** 异常，并显示消息 **这是一个负数**（`Its a negative number`）。最后，控制流进入 **finally** 语句，并显示消息 **控制流进入了 finally 块**（`Control entered in the finally block`）。

至此，本章结束。现在我们来总结本章的要点。

### 小结

在本章中，您学习了错误及其类型，例如语法错误、运行时错误和逻辑错误。此外，您还学习了异常以及处理异常的技术。最后，您学习了用户定义类。

在下一部分中，您将学习 **ASP.NET 4.0**，包括其不同版本、优点和新功能。

## ASP.NET 4.0 简介

### 第 1 章

### 本章内容：

- 探索 ASP.NET 的版本
- 描述 ASP.NET 的优点
- 探索 ASP.NET 4.0 中的新功能
- 探索 ASP.NET 4.0 Web 应用程序
- 解释 ASP.NET 4.0 提供程序模型
- 解释 ASP.NET 4.0 编码模型
- 实现代码共享
- 编译 ASP.NET 4.0 Web 应用程序
- 理解 ASP.NET 4.0 中的动态编译

ASP.NET 是一种用于为网站创建动态网页的技术。静态网页与动态网页的基本区别在于，静态网页无法动态（在运行时）更改其内容；而动态网页的外观和风格可以在运行时修改。ASP.NET 便于创建小型个人网站以及大型企业级网站。它是 Microsoft Active Server Pages (ASP) 技术的后继者，而 ASP 是 Microsoft 首个用于生成动态网页的服务器端脚本引擎。Microsoft 于 2002 年 1 月随 .NET Framework 1.0 发布了 ASP.NET 的第一个版本 ASP.NET 1.0。ASP.NET 构建在公共语言运行时 (CLR) 之上，这允许程序员使用 .NET Framework 支持的任何编程语言（如 C# 和 VB.NET）编写 ASP.NET 代码。

ASP.NET 的最新版本 ASP.NET 4.0 包含大量功能和增强，并且与其先前版本相比更加强大。ASP.NET 4.0 提供了用户友好的环境来编写托管应用程序，其中包括许多有助于创建代码的向导以及有用功能，例如上下文着色、集成联机帮助、自动完成和编辑时错误通知。

本章首先讨论 Microsoft ASP.NET 4.0 的版本和优点。接着讨论 ASP.NET 4.0 中引入的新功能。您还将了解 ASP.NET 4.0 中的提供程序模型和编码模型。最后讨论 ASP.NET 4.0 中的代码共享、编译和动态编译。

现在，我们从介绍 ASP.NET 的不同版本开始讨论。

### 探索 ASP.NET 的版本

到目前为止，市场上已发布四个 ASP.NET 版本：ASP.NET 1.0、ASP.NET 1.1、ASP.NET 2.0 和 ASP.NET 3.5。以下是对每个版本的简要描述：

- **ASP.NET 1.0：** 指 ASP.NET 的第一个版本。它于 2002 年 1 月 16 日与 Visual Studio.NET 2002 一起发布。
- **ASP.NET 1.1：** 指 ASP.NET 的第二个版本。它于 2003 年 4 月 24 日与 VS.NET 2003 一起发布。此版本新增的一些功能包括移动控件和自动输入验证。
- **ASP.NET 2.0：** 指 ASP.NET 的第三个版本。它于 2005 年 11 月 7 日与 VS 2005 一起发布。它向 ASP.NET 引入了若干新功能，包括母版页、个性化设置和 WebParts 控件。
- **ASP.NET 3.5：** 指 ASP.NET 的第四个版本，于 2007 年 11 月 19 日与 VS 2008 一起发布。此版本向 ASP.NET 引入了若干新功能，包括数据控件、将 ASP.NET AJAX 作为框架的一部分包含在内，以及通过新的 **LinqDataSource** 控件支持 LINQ。
- **ASP.NET 4.0：** 指 ASP.NET 的第五个版本，于 2010 年 4 月 12 日与 VS 2010 一起发布。此版本向 ASP.NET 引入了若干新功能，包括数据控件、Web Forms、Web.config 文件和样式表。

现在，我们来讨论 ASP.NET 的优点。

### 描述 ASP.NET 的优点

ASP.NET 从开发人员和最终用户的角度都提供了若干优点。ASP.NET 的一些优点如下：

- 支持健壮的数据库驱动功能
- 更快地执行网站
- 提供内存泄漏和崩溃保护
- 支持轻松部署
- 支持多种语言

下面各节将逐一详细讨论这些优点。
