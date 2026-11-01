
```csharp
comp.LongTaskAsync("input", 33);

Console.ReadLine();
}

static void Comp_LongTaskCompleted(object sender,
    LongTaskCompletedEventArgs e)
{
    Console.WriteLine("completed, result: {0}, thread: {1}", e.Output,
        Thread.CurrentThread.ManagedThreadId);
}
```

代码片段 AsyncComponent/Program.cs

对于 Windows 窗体应用程序，SynchronizationContext 被设置为 WindowsFormsSynchronizationContext——这就是事件处理程序代码会在同一线程中被调用的原因：

```csharp
WindowsFormsSynchronizationContext syncContext =
    new WindowsFormsSynchronizationContext();
SynchronizationContext.SetSynchronizationContext(syncContext);
```

## 总结

本章探讨了如何使用 System.Threading 命名空间编写使用多个线程的应用程序，以及如何使用 System.Threading.Tasks 命名空间编写使用多个任务的应用程序。在应用程序中使用多线程需要仔细规划。线程太多会导致资源问题，而线程不足则会使应用程序看起来反应迟钝且性能不佳。通过任务，你可以获得对线程的抽象。这种抽象有助于避免创建过多线程，因为线程是从池中复用的。

你已经看到了创建多个线程的各种方式，例如使用委托、定时器、ThreadPool 和 Thread 类。我们还探讨了多种同步技术，例如简单的 lock 语句，以及 Monitor、Semaphore 和 Event 类。你了解了如何使用 IAsyncResult 接口和基于事件的异步模式来编写异步模式。

.NET Framework 中的 System.Threading 命名空间为你提供了多种操作线程的方式；但这并不意味着 .NET Framework 会为你处理多线程的所有困难任务。你需要考虑线程优先级和同步问题。本章讨论了这些问题以及如何在 C# 应用程序中为它们编写代码。还探讨了与死锁和竞态条件相关的问题。

请记住，如果你打算在 C# 应用程序中使用多线程，那么仔细规划必须是你工作中的重要部分。

以下是关于线程的一些最终指南：

- 尽量将同步需求降至最低。同步是复杂的，并且会阻塞线程。如果你尽量避免共享状态，就可以避免同步。当然，这并非总是可能的。
- 类的静态成员应该是线程安全的。通常，.NET Framework 中的类就是这种情况。
- 实例状态不需要是线程安全的。为了获得最佳性能，同步最好在需要它的类外部使用，而不是与类的每个成员一起使用。.NET Framework 类的实例成员通常不是线程安全的。在 MSDN 库中，你可以在线程安全性部分找到每个类的相关文档信息。

下一章将介绍另一个 .NET 核心主题：安全性。

## 21

## 安全

### 本章内容

- 身份验证和授权
- 加密
- 资源访问控制
- 代码访问安全

安全性有几个关键要素，你在确保应用程序安全时需要考虑这些要素。其中一个要素是应用程序的用户。访问应用程序的确实是用户本人，还是冒充用户的人？如何信任这个用户？正如你将在本章中看到的，首先需要对用户进行身份验证，然后进行授权，以验证该用户是否被允许使用所请求的资源。

那么通过网络存储或发送的数据呢？是否有人可能通过使用网络嗅探器之类的工具访问这些数据？在这里，数据加密非常重要。一些技术，例如 Windows Communication Foundation (WCF)，通过简单的配置即可提供加密功能，因此你可以了解底层发生了什么。

另一个方面是应用程序本身。如果应用程序由 Web 提供商托管，会怎么样？如何限制应用程序对服务器造成危害？

本章探讨了 .NET 中可用于帮助您管理安全性的功能，并向您展示 .NET 如何保护您免受恶意代码的侵害、如何管理安全策略，以及如何以编程方式访问安全子系统。

## 身份验证和授权

安全性的两个基本支柱是身份验证和授权。身份验证是识别用户的过程，随后进行的授权用于验证被识别的用户是否被允许访问特定资源。

### 身份和主体

您可以通过使用身份来标识运行应用程序的用户。WindowsIdentity 类表示 Windows 用户。如果您不通过 Windows 账户标识用户，则可以使用实现 IIdentity 接口的其他类。通过该接口，您可以访问用户的名称、有关用户是否经过身份验证的信息以及身份验证类型。

主体是一个包含用户身份及用户所属角色的对象。IPrincipal 接口定义了属性 Identity（返回 IIdentity 对象）和方法 IsInRole，通过后者您可以验证用户是否为特定角色的成员。角色是拥有相同安全权限的用户的集合，也是用户管理的单位。角色可以是 Windows 组，也可以只是您定义的字符串集合。

.NET 提供的主体类是 WindowsPrincipal 和 GenericPrincipal。您还可以创建实现 IPrincipal 接口的自定义主体类。

在下面的示例中，您将创建一个控制台应用程序，该应用程序提供对应用程序中主体的访问，进而使您能够访问底层 Windows 账户。您需要导入 System.Security.Principal 和 System.Threading 命名空间。首先，您必须指定 .NET 应自动将主体与底层 Windows 账户关联起来。必须这样做是因为 .NET 出于安全原因不会自动填充线程的 CurrentPrincipal 属性。您可以这样做：

```csharp
using System;
using System.Security.Principal;
using System.Threading;

namespace Wrox.ProCSharp.Security
{
    class Program
    {
        static void Main()
        {
            AppDomain.CurrentDomain.SetPrincipalPolicy(PrincipalPolicy.WindowsPrincipal);
        }
    }
}
```

代码片段 WindowsPrincipal/Program.cs

可以使用 WindowsIdentity.GetCurrent() 来访问 Windows 账户详细信息；但是，该方法最适合在您仅查看一次主体时使用。如果您想多次访问主体，更有效的做法是设置策略，以便当前线程为您提供对主体的访问权限。如果使用 SetPrincipalPolicy 方法，则指定当前线程中的主体应持有 WindowsIdentity 对象。所有标识类（例如 WindowsIdentity）都实现 IIdentity 接口。该接口包含三个属性（AuthenticationType、IsAuthenticated 和 Name），供所有派生标识类实现。

添加代码以从 Thread 对象访问主体的属性：

```csharp
WindowsPrincipal principal =
    (WindowsPrincipal)Thread.CurrentPrincipal;
WindowsIdentity identity = (WindowsIdentity)principal.Identity;
Console.WriteLine("IdentityType: " + identity.ToString());
Console.WriteLine("Name: {0}", identity.Name);
Console.WriteLine("Users?: {0} ", principal.IsInRole(WindowsBuiltInRole.User));
Console.WriteLine("Administrators?: {0}", principal.IsInRole(WindowsBuiltInRole.Administrator));
Console.WriteLine("Authenticated: {0}", identity.IsAuthenticated);
Console.WriteLine("AuthType: {0}", identity.AuthenticationType);
Console.WriteLine("Anonymous?: {0}", identity.IsAnonymous);
Console.WriteLine("Token: {0}", identity.Token);
}
}
```
