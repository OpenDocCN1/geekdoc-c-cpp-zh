

## 清单 19.24：安全调用用户界面对象

```csharp
using System;
using System.Windows;
using System.Windows.Threading;

public static class UIAction
{
    public static void Invoke<T>(
        Action<T> action, T parameter)
    {
        Invoke(() => action(parameter));
    }

    public static void Invoke(Action action)
    {
        DispatcherObject dispatcher =
            Application.Current;

        if (dispatcher == null
            || dispatcher.CheckAccess()
            || dispatcher.Dispatcher == null
        )
        {
            action();
        }
        else
        {
            SafeInvoke(action);
        }
    }

    // We want to catch all exceptions here
    // so we can rethrow
    private static void SafeInvoke(Action action)
    {
        Exception exceptionThrown = null;
        Action target = () =>
        {
            try
            {
                action();
            }
            catch (Exception exception)
            {
                exceptionThrown = exception;
            }
        };

        Application.Current.Dispatcher.Invoke(target);
        if (exceptionThrown != null)
        {
            throw exceptionThrown;
        }
    }
}
```

Listing 19.24 中的 UIAction 的一个额外功能是对可能发生在 UI 线程上的任何异常进行“封送”。SafeInvoke() 将所有请求的委托调用包装在 try/catch 块中，如果抛出异常，它会保存异常，然后在上下文返回到调用线程后重新抛出它。这样一来，UIAction 就避免了在 UI 线程上抛出未处理的异常。

## 高级主题

### 使用 STAThreadAttribute 控制 COM 线程模型

使用 COM 时，四种不同的单元线程模型决定了 COM 对象之间调用的线程规则。幸运的是，只要程序不调用 COM 组件，这些规则——以及随之而来的复杂性——就已从 .NET 中消失。处理 COM Interop 的一般方法是通过用 System.STAThreadAttribute 装饰进程的 Main 方法，将所有 .NET 组件置于主单线程单元中。这样一来，调用大多数 COM 组件时就不需要跨越单元边界。此外，除非进行 COM Interop 调用，否则不会发生单元初始化。这种方法的注意事项是，所有其他线程（包括 Task 的线程）都将默认使用多线程单元（MTA）。因此，从主线程以外的其他线程调用 COM 组件时需要小心。

COM Interop 不一定是开发者的显式操作。Microsoft 通过创建运行时可调用包装器（RCW）而不是在托管代码中重写所有 COM 功能，实现了 .NET Framework 中的许多组件。因此，COM 调用往往是在不知情的情况下进行的。为了确保这些调用始终从单线程单元进行，通常的良好做法是将所有 Windows Forms 可执行文件的主方法用 System.STAThreadAttribute 装饰。

## 摘要

本章首先介绍了各种同步机制以及可用于防止竞态条件的多种类。掌握这些知识后，我们能够进一步深入研究多种额外的多线程模式，包括以下内容：

- 异步编程模型 (APM)：通常由低级库公开，作为异步调用长时间运行方法的一种方式。
- 基于事件的异步模式 (EAP)：类似于 EAP，但用于更高级别的编程。EAP 公开了一种用于异步编程的 API，包括对取消和进度通知的支持。
- 后台工作线程模式：BackgroundWorker 类提供的 API，允许调用者将异步模式强加于长时间运行的方法，即使设计者未实现此类模式。

鉴于除了 TPL 提供的模式之外还有众多模式可供选择，知道该选择哪一种可能会有些令人困惑。通常，选择 API 提供的模式（例如 APM 或 EAP）比使用 TPL 来异步执行方法更好。但是，在 EAP 的情况下，TPL 提供了利用 EAP 的调用支持，因此如果 TPL 可用，建议使用两者的组合。选择使用后台工作线程模式而不是 TPL 则要微妙一些。只要 BackgroundWorker 提供了您所需的一切，开发者偏好就是一个可接受的决定因素。一旦您需要额外功能，TPL 就更合适。但是，如果所有注册的侦听器（用于取消、进度和完成）都是通过仔细使用匿名方法和闭包来完成的，也请考虑使用 TPL，因为 TPL 可能更易于维护。但是，如果情况并非如此，请考虑改用 BackgroundWorker，因为您可以轻松注册成员而无需依赖闭包。

下一章将探讨另一种复杂的 .NET 技术：使用 P/Invoke 将调用从 .NET 封送到托管代码。此外，它还介绍了一种称为不安全代码的概念，C# 使用它直接访问内存指针，如同在非托管代码（例如 C++）中一样。

## 20 平台互操作性和不安全代码

C# 功能强大，但有时仍然不够，您需要摆脱其提供的所有安全性，回到内存地址和指针的世界中。C# 以三种方式支持这一点。第一种方式是通过平台调用 (P/Invoke) 调用非托管 DLL 公开的 API。第二种是通过不安全代码，它能够访问内存指针和地址。代码经常组合使用这些功能。第三种方式（本文未涉及）是通过 COM 互操作性。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_863_0.png)

本章以一个小程序作为高潮，用于确定计算机是否为虚拟计算机。该代码要求您执行以下操作。

- 1. 调用操作系统 DLL 并请求分配一部分内存用于执行指令。
- 2. 将一些汇编指令写入分配的区域。
- 3. 将地址位置注入汇编指令中。
- 4. 执行汇编代码。

除了此处介绍的 P/Invoke 和不安全代码结构之外，最终清单展示了 C# 的全部功能，以及非托管代码的功能仍可从 C# 和托管代码中访问的事实。

### 初学者主题

### 什么是虚拟计算机？

虚拟计算机（或虚拟机），也称为客户机计算机，是通过在主机操作系统上运行并与主机计算机硬件交互的软件进行虚拟化或模拟的。例如，虚拟计算机软件（如 VMware Workstation 和 Microsoft Virtual PC）可以安装在运行较新版本 Windows 的计算机上。安装软件后，用户可以在软件中配置客户机计算机，启动它，并安装操作系统，就像它是一台真实计算机，而不仅仅是通过软件虚拟化的计算机一样。

### 平台调用

无论开发者是试图调用其现有非托管代码的库、访问操作系统中未在任何托管 API 中公开的非托管代码，还是试图为特定算法实现最大性能（该算法通过避免类型检查和垃圾回收的运行时开销而运行得更快），总有一天她必须调用非托管代码。CLI 通过 P/Invoke 提供此功能。使用 P/Invoke，您可以调用非托管 DLL 中导出函数的 API。

本节中调用的所有 API 都是 Windows API。尽管相同的 API 在其他平台上不可用，但开发者仍可针对其平台原生的 API 或调用其自身 DLL 时使用 P/Invoke。准则和语法相同。

### 声明外部函数

一旦确定了目标函数，P/Invoke 的下一步就是使用托管代码声明该函数。与属于类的所有常规方法一样，您需要在类的上下文中声明目标 API，但使用 extern 修饰符。清单 20.1 演示了如何执行此操作。

```
LISTING 20.1: Declaring an External Method

using System;
using System.Runtime.InteropServices;

class VirtualMemoryManager
{
    [DllImport("kernel32.dll", EntryPoint="GetCurrentProcess")]
    internal static extern IntPtr GetCurrentProcessHandle();
}
```

在此示例中，该类是 VirtualMemoryManager，因为它将包含与内存管理相关的函数。（此特定函数可直接从 System.Diagnostics.Process 类获取，因此在实际代码中无需声明它。）

extern 方法始终是静态的，并且不包含任何实现。相反，随方法声明一起提供的 DllImport 特性指向实现。至少，该特性需要定义该函数的 DLL 名称。运行时从方法名称确定函数名称。但是，可以使用 EntryPoint 命名参数提供函数名称来覆盖此默认值。（.NET 平台将自动尝试调用 Unicode [...W] 或 ASCII [...A] API 版本。）

在此示例中，外部函数 GetCurrentProcess() 为当前进程检索一个伪句柄，您将在虚拟内存分配调用中使用它。以下是非托管声明：

```
HANDLE GetCurrentProcess();
```

