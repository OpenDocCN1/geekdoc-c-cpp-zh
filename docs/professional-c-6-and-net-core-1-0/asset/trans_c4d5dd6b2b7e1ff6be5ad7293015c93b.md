

```csharp
};
context.Menus.Add(mInvalid);
records = await context.SaveChangesAsync();
WriteLine($"{records} records added");
tx.Commit();
}
catch (DbUpdateException ex)
{
WriteLine($"{ex.Message}");
WriteLine($"{ex?.InnerException.Message}");
WriteLine("rolling back...");
tx.Rollback();
}
WriteLine();
```

当你运行应用程序时，你可以看到，尽管多次调用了 SaveChangesAsync 方法，但没有添加任何记录。SaveChangesAsync 的第一次返回列出添加了一条记录，但该记录随后基于 Rollback 被移除。根据隔离级别的设置，更新的记录只能在事务内回滚完成之前看到，而在事务外则看不到。

```text
TwoSaveChangesWithOneTxAsync
1 records added
An error occurred while updating the entries. See the inner exception for details.
The INSERT statement conflicted with the FOREIGN KEY constraint "FK_Menu_MenuCard_MenuCardId".
The conflict occurred in database 'MenuCards',
table "mc.MenuCards", column 'MenuCardId'.
rolling back...
```

> 注意 使用 BeginTransactionAsync 方法，你还可以为隔离级别提供一个值，以指定数据库所需的隔离要求和锁。第 37 章将讨论隔离级别。

## 小结

本章向你介绍了 Entity Framework Core 的特性。你了解了对象上下文如何保留有关已检索和更新实体的信息，以及如何将更改写入数据库。你还看到了如何使用迁移从 C# 代码创建和更改数据库架构。为了定义架构，你已经看到了如何使用数据注解完成数据库映射，并且你还了解了与注解相比提供更多功能的 Fluent API。

你已经了解了在多个用户处理同一条记录时应对冲突的可能性，以及如何隐式或显式地使用事务来获得更多的事务控制。

下一章将展示如何使用 Windows 服务来创建随系统自动启动的程序。你可以在 Windows 服务中使用 Entity Framework。

## 39 Windows 服务

### 本章内容

- Windows 服务的架构
- 创建 Windows 服务程序
- Windows 服务的安装程序
- Windows 服务的控制程序
- Windows 服务的故障排除

### Wrox.com 本章代码下载

本章的 wrox.com 代码下载可以在 [www.wrox.com/go/professionalcsharp6](http://www.wrox.com/go/professionalcsharp6) 的 Download Code 标签页找到。代码位于 Chapter 39 下载中，并根据本章中的名称单独命名。

- Quote Server
- Quote Client
- Quote Service
- Service Control

### 什么是 Windows 服务？

Windows 服务是可以在启动时自动启动的程序，无需任何人登录机器。如果你需要让程序在没有用户交互的情况下启动，或者需要以不同于交互用户的其他用户（可以是拥有更多权限的用户）运行，则可以创建 Windows 服务。一些示例包括 WCF 主机（如果由于某种原因无法使用 Internet Information Services (IIS)）、缓存网络服务器数据的程序，或在后台整理本地磁盘数据的程序。

本章首先介绍 Windows 服务的架构，创建一个承载网络服务器的 Windows 服务，并为你提供启动、监视、控制和排查 Windows 服务的信息。

如前所述，Windows 服务是可以在操作系统启动时自动启动的应用程序。这些应用程序可以在没有交互用户登录系统的情况下运行，并在后台进行一些处理。

例如，在 Windows Server 上，系统网络服务应该无需用户登录服务器即可从客户端访问；而在客户端系统上，服务使你能够执行诸如在线获取新软件版本或对本地磁盘执行一些文件清理等操作。

你可以将 Windows 服务配置为使用专门配置的用户帐户或系统用户帐户（一种拥有比系统管理员更多权限的用户帐户）运行。

> 注意 除非另有说明，否则当我提到服务时，我指的是 Windows 服务。

以下是一些服务的示例：

- Simple TCP/IP Services 是一个承载一些小型 TCP/IP 服务器的服务程序：echo、daytime、quote 等。
- World Wide Web Publishing Service 是 IIS 的一项服务。
- Event Log 是一项将消息记录到事件日志系统的服务。
- Windows Search 是一项在磁盘上创建数据索引的服务。
- Superfetch 是一项将常用应用程序和库预加载到内存中的服务，从而缩短这些应用程序的启动时间。

你可以使用如图 39.1 所示的服务管理工具查看系统上的所有服务。在“开始”屏幕中输入“服务”即可进入该程序。

![图 39.1](img/3d365b72b289213a91ade7eb366b8f35_1485_0.png)

图 39.1

> 注意 你不能使用 .NET Core 创建 Windows 服务；你需要 .NET Framework。要控制服务，你可以使用 .NET Core。

### Windows 服务架构

![图 39.2](img/3d365b72b289213a91ade7eb366b8f35_1487_0.png)

图 39.2

启动时，每个设置为自动启动的服务所对应的进程都会被启动，因此该进程的主函数会被调用。服务负责为其每个服务注册服务主函数。主函数是服务程序的入口点，在此函数中，必须使用 SCM 注册服务主函数的入口点。

### 主函数、服务主函数和处理函数

服务的主函数是程序的正常入口点，即 Main 方法。服务的主函数可能注册多个服务主函数。服务主函数包含服务的实际功能，必须为其提供的每个服务注册一个服务主函数。一个服务程序可以在单个程序中提供许多服务；例如，

```text
<windows>\system32\services.exe is the service program that includes Alerter, Application Management, Computer Browser, and DHCP Client, among other items.
```

SCM 为每个应启动的服务调用服务主函数。服务主函数的一项重要任务是向 SCM 注册处理函数。

处理函数是服务程序的第三部分。处理函数必须响应来自 SCM 的事件。服务可以被停止、挂起和恢复，处理函数必须对这些事件做出反应。

在处理函数向 SCM 注册后，服务控制程序可以向 SCM 发送请求以停止、挂起和恢复服务。服务控制程序独立于 SCM 和服务本身。操作系统包含许多服务控制程序，例如前面图 39.1 中显示的 Microsoft 管理控制台 (MMC) 服务管理单元。你也可以编写自己的服务控制程序；一个很好的例子是图 39.3 中显示的、在 MMC 中运行的 SQL Server 配置管理器。

![图 39.3](img/3d365b72b289213a91ade7eb366b8f35_1488_0.png)

图 39.3

### 服务控制程序

顾名思义，使用服务控制程序你可以停止、挂起和恢复服务。为此，你可以向服务发送控制代码，处理函数应对这些事件做出反应。你还可以询问服务的实际状态（服务是否正在运行、已挂起或处于某种故障状态），并实现一个响应自定义控制代码的自定义处理函数。

### 服务配置程序

因为服务必须在注册表中进行配置，所以你不能对服务使用 xcopy 安装。注册表包含服务的启动类型，可以设置为自动、手动或禁用。你还需要配置服务程序的用户和服务的依赖项——例如，任何必须在当前服务启动之前启动的服务。所有这些配置都在服务配置程序中完成。安装程序可以使用服务配置程序来配置服务，但该程序也可以稍后用于更改服务配置参数。

### Windows 服务的类

在 .NET Framework 中，你可以在 System.ServiceProcess 命名空间中找到实现服务三部分的服务类：

- 你必须继承 ServiceBase 类来实现服务。ServiceBase 类用于注册服务并响应启动和停止请求。

