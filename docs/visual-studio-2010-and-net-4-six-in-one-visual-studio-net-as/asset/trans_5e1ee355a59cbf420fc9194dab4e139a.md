
![](img/b5597c749e848b27b0d305153ae16106_1065_0.png)

# 图 22-1：IronPython 运行时程序集

> 你可以在操作系统的 Program Files 文件夹（x86 文件夹）下直接找到带有 IronPython 前缀的文件夹。在编写本文时，专门为 Visual Studio 2010 Beta 2 创建了独立的 IronPython 发行版本。请检查 IronPython 主页以获取最新版本。

添加一个新的文本文件并将其命名为 Quadratic.py，其中 .py 是 IronPython 程序文件的标准扩展名。该文件应位于控制台应用程序启动所在的文件夹。将 Quadratic.py 的 **Build Action**（生成操作）属性设置为 **Content**（内容），并将 **Copy to Directory**（复制到目录）属性设置为 **Copy Always**（始终复制）。

列表 22-4 显示了你应该复制到 Quadratic.py 文件中的内容。

# 列表 22-4：Quadratic.py

```python
import math

def SolveQuadratic(A, B, C):
    determ = B*B - 4*A*C
    solution1 = 0.0
    solution2 = 0.0
    hasSolution = determ >= 0.0
    if hasSolution:
        solution1 = (-B + math.sqrt(determ))/(2*A)
        solution2 = (-B - math.sqrt(determ))/(2*A)
    return hasSolution, solution1, solution2
```

代码文件 [Quadratic.py] 可在 Wrox.com 下载。

这段短小的 Python 代码解决了形式为 Ax² + Bx + c = 0 的二次方程，并以元组的形式获取结果，包含一个布尔值（是否有解）和两个数字（两个可能的解）。

使用 Module1.vb 文件复制列表 22-5 中的代码来调用该 Python 代码段。。

# 列表 22-5：IronPythonRunner 的 Module1.vb 文件

```vbnet
Option Strict Off

Imports IronPython.Hosting

Module Module

Sub Main()
    Dim ipy As Object = Python.CreateRuntime()
    Dim calculator As Object = ipy.UseFile("Quadratic.py")
    SolveQuadratic(calculator, 1.0, 2.0)
    SolveQuadratic(calculator, 2.0, 15.0, 6.0)
End Sub

Sub SolveQuadratic(ByVal Calculator Object,
ByVal A As Double,
ByVal B As Double,
ByVal C As Double)
    Dim result As Object = calculator.SolveQuadratic(A, B, C)
    Console.WriteLine("The quadratic equation (0)*x + (1)*x + (2) = 0*",
    A, B, C)

    If result(0) Then
        Console.WriteLine(" has the following solutions:")
        Console.WriteLine("#1: (0), result(1))")
        Console.WriteLine("#2: (0), result(2))")
    Else
        Console.WriteLine(" has no solution.")
    End If
    Console.WriteLine()
End Sub
```

代码文件 [Module1.vb] 可在 Wrox.com 下载。

代码非常简单。位于 IronPython.Hosting 命名空间的 Python 对象负责管理运行时环境。你可以获取一个对象的引用（在此上下文中命名为 calculator），以访问 Quadratic 微程序定义的操作：

```vb
Dim ipy As Object = Python.CreateRuntime()
Dim calculator As Object = ipy.UseFile("Quadratic.py")
```

你可以通过 calculator 对象调用 Python 代码段中定义的 SolveQuadratic 操作：

```vb
Dim result As Object = calculator.SolveQuadratic(A, B, C)
```

结果将是一个包含三个值的元组，你可以从 0 到 2 对其进行索引。图 22-2 显示了控制台应用程序的输出。

![](img/b5597c749e848b27b0d305153ae16106_1067_0.png)

**图 22-2：应用程序的输出**

> IronPython 运行时带简短的教程。打开安装文件夹下的 Tutorial.html 文件，并配合 quadratic.py 和 Module.vb 文件进行练习。你可以在 http://docs.python.org/tutorial/ 找到关于 Python 语言的通用或更详细的教程。

## 继承

继承是一个强大的面向对象原则，当你创建 .NET 应用程序或组件时总是直接或间接地使用它。Visual Basic 在面向对象编程（OOP）方面经历了长期，但第一个 Visual Basic .NET 版本（2002）让语言能够完全实现这些原则。.NET Framework 2.0 和 Visual Basic 2005 引入了泛型，提高了开发性能，以及代码的可重用性。泛型有时会让你感到惊讶，因为某些操作是非法的，即使你认为它们是允许的。

## 类型替换

如果你看到下面的 Visual Basic 控制台应用程序，你会发现它是这样运行的：

```vb
Module Module

Public strings As IList(Of String) = New List(Of String)
Public objects As IList(Of Object) = strings

Sub Main()
    strings.Add("Hello")
```

```vb
strings.Add("World")
```

For Each item In objects
    Console.WriteLine(item)
Next
End Sub
```
