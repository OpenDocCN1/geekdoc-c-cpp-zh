
## 25
## Windows 服务
## 本章内容
- Windows 服务的体系结构
- Windows 服务安装程序
- Windows 服务控制程序
- Windows 服务故障排除

Windows 服务是在启动时可以自动启动的程序，无需任何人登录计算机。下面的部分将介绍 Windows 服务的体系结构。本章其余部分将向你展示如何创建、监视、控制和排查 Windows 服务。

## 什么是 WINDOWS 服务？

Windows 服务是操作系统启动时可以自动启动的应用程序。这些应用程序可以在没有交互式用户登录系统的情况下运行，并在后台执行一些处理工作。

例如，在 Windows Server 上，系统网络服务应该能够被客户端访问，而无需用户登录服务器。在客户端系统上，服务可以让你从 Internet 获取新版本的软件，或清理本地磁盘上的文件。

你可以将 Windows 服务配置为从专门配置的用户帐户运行，也可以从系统用户帐户运行——系统用户帐户拥有甚至超过系统管理员的权限。

![](img/d7d2ffa0a76feaab821930e95daace93_728_0.png)

下面是一些服务示例：
- Simple TCP/IP Services 是一个承载一些小型 TCP/IP 服务器的服务程序：echo、daytime、quote 等。
- World Wide Web Publishing Service 是 Internet Information Server（IIS）的服务。
- Event Log 是用于将消息记录到事件日志系统中的服务。
- Windows Search 是用于创建磁盘上数据索引的服务。

你可以使用图 25-1 所示的“服务”管理工具查看系统上的所有服务。可以在“管理工具”中找到此程序。

![](img/d7d2ffa0a76feaab821930e95daace93_729_0.png)

图 25-1

## WINDOWS 服务体系结构

运行 Windows 服务需要三类程序：
- 服务程序
- 服务控制程序
- 服务配置程序

服务程序本身提供你所需的实际功能。通过服务控制程序，可以向服务发送控制请求，例如启动、停止、暂停和继续。通过服务配置程序，可以安装服务；服务文件会被复制到文件系统中，相关信息会被写入注册表，并将其配置为服务。虽然 .NET 组件可以通过简单的 xcopy 进行安装——因为它们不需要向注册表写入信息——但服务的安装需要进行注册表配置。服务配置程序还可以在之后用于更改该服务的配置。

下面的子节将讨论 Windows 服务的这三个组成部分。

### 服务程序

在查看服务的 .NET 实现之前，让我们先从独立于具体实现的角度，了解 Windows 服务的体系结构以及服务的内部功能。

### 服务控制程序

顾名思义，使用服务控制程序可以控制服务。要停止、暂停和恢复服务，可以向服务发送控制代码，而处理程序应对这些事件做出响应。还可以查询服务的实际状态，并实现一个能够响应自定义控制代码的自定义处理程序。

### 服务配置程序

由于服务必须在注册表中进行配置，因此不能对服务使用 xcopy 安装。注册表包含服务的启动类型，可以将其设置为自动、手动或禁用。还需要配置服务程序的用户以及服务的依赖项——例如，必须在此服务启动之前启动的服务。所有这些配置都在服务配置程序中完成。安装程序可以使用服务配置程序来配置服务，但之后也可以使用该程序更改服务配置参数。

## Windows 服务的类

在 .NET Framework 中，可以在 System.ServiceProcess 命名空间中找到实现服务三个组成部分的服务类：
- 必须从 ServiceBase 类继承才能实现服务。ServiceBase 类用于注册服务，并响应启动和停止请求。
- ServiceController 类用于实现服务控制程序。通过此类，可以向服务发送请求。
- ServiceProcessInstaller 和 ServiceInstaller 类，正如它们的名称所示，是用于安装和配置服务程序的类。

现在可以创建一个新服务了。

## 创建 WINDOWS 服务程序

本章创建的服务承载一个报价服务器。每当客户端发出请求时，报价服务器都会从报价文件中返回一条随机报价。解决方案的第一部分使用三个程序集：一个用于客户端，两个用于服务器。图 25-4 概述了该解决方案。QuoteServer 程序集包含实际功能。服务将报价文件读取到内存缓存中，并借助套接字服务器响应报价请求。QuoteClient 是一个 WPF 富客户端应用程序。此应用程序创建客户端套接字，以便与 QuoteServer 通信。第三个程序集是真正的服务。QuoteService 启动和停止 QuoteServer；该服务负责控制服务器。

![](img/d7d2ffa0a76feaab821930e95daace93_731_0.png)

图 25-4

### 为服务创建核心功能

你可以在 Windows 服务中构建任何功能，例如扫描文件以执行备份或病毒检查，或者启动 WCF 服务器。不过，所有服务程序都有一些共同点。程序必须能够启动（并返回调用方）、停止和暂停。本节将使用套接字服务器介绍这类实现。

在 Windows 7 中，可以将 Simple TCP/IP Services 作为 Windows 组件的一部分进行安装。Simple TCP/IP Services 的一部分是“每日报价”（quote of the day），即 qotd TCP/IP 服务器。这个简单的服务监听端口 17，并使用文件 <windir>\system32\drivers\etc\quotes 中的随机消息响应每个请求。示例服务将构建一个类似的服务器。与返回 ASCII 字符串的老式 qotd 服务器不同，示例服务器返回 Unicode 字符串。

首先，创建一个名为 QuoteServer 的 Class Library，并实现服务器代码。下面将逐步介绍文件 QuoteServer.cs 中 QuoteServer 类的源代码：

```
```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading;

namespace Prox.ProSharp.WinServices
{
    public class QuoteServer
    {
        private TcpListener listener;
        private int port;
        private string filename;
        private List<string> quotes;
        private Random random;
        private Thread listenerThread;
```
```

QuoteServer() 构造函数进行了重载，因此可以向调用传入文件名和端口。仅传入文件名的构造函数使用服务器的默认端口 7890。默认构造函数将报价的默认文件名定义为 quotes.txt：

```
```csharp
public QuoteServer()
    : this("quotes.txt")
{
}
public QuoteServer(string filename)
    : this(filename, 7890)
{
}
public QuoteServer(string filename, int port)
{
    this.filename = filename;
    this.port = port;
}
```
```
