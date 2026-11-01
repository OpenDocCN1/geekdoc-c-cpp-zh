
## 版本号

程序集具有四部分版本号，例如 1.1.400.3300。各部分为 <Major>.<Minor>.<Build>.<Revision>。

这些数字的使用方式取决于应用程序的配置。

> 一个好的做法是在与之前版本不兼容的更改时修改主版本号或次版本号，而在兼容性更改时仅修改内部版本号或修订号。这样可以认为将程序集重定向到仅内部版本号和修订号发生变化的新版本是安全的。

使用 Visual Studio 2010，可以通过项目设置中的程序集信息来定义程序集的版本号。项目设置会将程序集属性 [AssemblyVersion] 写入文件 AssemblyInfo.cs：

```
[assembly: AssemblyVersion("1.0.0.0")]
```

如果不想定义全部四个版本号，也可以在第三或第四位放置星号：

```
[assembly: AssemblyVersion("1.0.*")]
```

使用此设置，前两个数字指定主版本号和次版本号，而星号 (*) 表示内部版本号和修订号自动生成。内部版本号是自 2000 年 1 月 1 日以来的天数，修订号是午夜以来秒数除以二。虽然自动版本控制在开发期间可能有帮助，但在发布前最好定义一个特定的版本号。

此版本存储在清单的 .assembly 部分中。

在客户端应用程序中引用程序集会将引用程序集的版本存储在客户端应用程序的清单中。

## 以编程方式获取版本

为了能够从客户端应用程序检查所使用的程序集的版本，请向之前创建的 SharedDemo 类添加只读属性 FullName，以返回程序集的强名称。为了方便使用 Assembly 类，必须导入 System.Reflection 命名空间：

```
public string FullName
{
    get
    {
        return Assembly.GetExecutingAssembly().FullName;
    }
}
```

代码片段 SharedDemo/SharedDemo.cs

Assembly 类的 FullName 属性包含类名、版本、区域性和公钥标记，如在客户端应用程序中调用 FullName 时以下输出所示。

在客户端应用程序中，只需在创建共享组件后在 Main() 方法中添加对 FullName 的调用：

```
static void Main()
{
    var quotes = new SharedDemo("Quotes.txt");
    Console.WriteLine(quotes.FullName);
}
```

代码片段 Client/Program.cs

请务必使用 gacutil 再次在 GAC 中注册共享程序集 SharedDemo 的新版本。如果找不到引用的版本，将会得到 System.IO.FileLoadException，因为绑定到正确的程序集失败。

运行成功后，可以看到引用程序集的完整名称：

```
SharedDemo, Version=1.0.0.0, Culture=neutral, PublicKeyToken= f946433fdae2512d
```

此客户端程序现在可用于测试此共享组件的不同配置。

## 绑定到程序集版本

使用配置文件，可以指定绑定应发生在共享程序集的不同版本上。假设你创建了共享程序集 SharedDemo 的新版本，主版本号和次版本号为 1.1。也许你不想重建客户端，只想让现有客户端使用程序集的新版本即可。这在共享程序集修复了错误或你只想摆脱旧版本因为新版本兼容的情况下很有用。

通过运行 gacutil.exe，可以看到为 SharedDemo 程序集安装了 1.0.0.0 和 1.0.3300.0 版本：

```
> gacutil -l SharedDemo

Microsoft (R) .NET Global Assembly Cache Utility. Version 4.0.21006.1
Copyright (c) Microsoft Corporation. All rights reserved.

The Global Assembly Cache contains the following assemblies:
SharedDemo, Version=1.0.0.0, Culture=neutral, PublicKeyToken=f946433fdae2512d,
processorArchitecture=x86
SharedDemo, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=f946433fdae2512d, processorArchitecture=x86

Number of items = 2
```

图 18-14 显示了客户端应用程序的清单，其中客户端引用了程序集 SharedDemo 的 1.0.0.0 版本。

现在再次需要应用程序配置文件。如前所述，被重定向的程序集需要使用 <assemblyIdentity> 元素指定。此元素使用名称、区域性和公钥标记来标识程序集。对于重定向到不同版本，使用 <bindingRedirect> 元素。oldVersion 属性指定应重定向到新版本的程序集版本。使用 oldVersion 可以指定一个范围，如所示，所有从 1.0.0.0 到 1.0.3300.0 的程序集都应被重定向。newVersion 属性指定新版本。

![](img/d7d2ffa0a76feaab821930e95daace93_517_0.png)

图 18-14

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="SharedDemo" culture="neutral" publicKeyToken="f946433fdae2512d" />
        <bindingRedirect oldVersion="1.0.0.0-1.0.3300.0" newVersion="1.0.3300.0" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

## 覆盖发布者策略

使用发布者策略，共享程序集的发布者保证新版本与旧版本兼容。正如你所知，从传统 DLL 的更改来看，这样的保证并不总是成立。也许除了一个应用程序外，所有应用程序都可以使用新的共享程序集。为了修复对新版本有问题的那个应用程序，可以通过使用应用程序配置文件来覆盖发布者策略。

你可以通过添加带有属性 apply="no" 的 XML 元素 <publisherPolicy> 来禁用发布者策略。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="SharedDemo" culture="neutral" publicKeyToken="f946433fdae2512d" />
        <publisherPolicy apply="no" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

代码片段 Client/App.config

通过禁用发布者策略，可以在应用程序配置文件中配置不同的版本重定向。

## 运行时版本

安装和使用多个版本不仅适用于程序集，也适用于 .NET 运行时（CLR）。CLR 的 1.0、1.1、2.0 和 4.0（以及更高版本）可以在同一操作系统上并排安装。Visual Studio 2010 应用程序目标运行在 CLR 2.0 上的 .NET 2.0、3.0 和 3.5，以及 CLR 4.0 上的 .NET 4。

如果应用程序使用 CLR 2.0 构建，它可能在仅安装了 CLR 4.0 的系统上无需更改即可运行。反之则不成立，如果应用程序使用 CLR 4.0 构建，它无法在仅安装了 CLR 2.0 的系统上运行。

在应用程序配置文件中，不仅可以重定向引用程序集的版本，还可以定义运行时所需的版本。你可以在应用程序配置文件中指定应用程序所需的版本。元素 <supportedRuntime> 标记应用程序支持的运行时版本。<supportedRuntime> 元素的顺序定义了如果系统上存在多个运行时版本时的首选项。此处的配置优先使用 .NET 4 运行时，同时也支持 2.0。请记住，要实现这一点，应用程序必须使用目标框架 .NET 2.0、3.0 或 3.5 构建。

```xml
<?xml version="1.0"?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0.21006" />
    <supportedRuntime version="v2.0.50727" />
  </startup>
</configuration>
```

## 摘要

程序集是 .NET 平台的新安装单元。微软从以前架构的问题中吸取了教训，并进行了彻底重新设计以避免旧问题。本章讨论了程序集的特性：它们是自描述的，并且不需要类型库和注册表信息。
