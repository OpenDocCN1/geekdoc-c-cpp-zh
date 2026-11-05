
- **Internet 连接共享 (ICS) 服务** - ICS 使连接到 Internet 的一台设备可用作其他设备的接入点。访问可通过以太网宽带、蜂窝服务或其他网关进行。

- **路由和远程访问服务** - 此服务使创建应用程序成为可能，这些应用程序可管理 Windows 操作系统的**远程访问**和路由功能。它允许该计算机充当网络路由器。

## 25.1.7 创建 Windows 服务

开发人员通常将服务用于需要在后台运行的功能，例如监控性能数据并对指定阈值作出反应的能力。服务也可以创建为 **Microsoft Visual Studio 项目**，开发代码来指定可以向服务发送哪些命令，以及收到这些命令后采取哪些操作。创建并生成应用程序后，可以通过运行命令行实用工具 InstallUtil.exe，然后传递该服务可执行文件的路径，将其安装为服务。然后使用服务控制管理器配置该服务。或者，可以使用服务器资源管理器中的“服务”节点或 ServiceController 类来配置服务。

### 使用 C# 创建 Windows 服务

- **步骤 1** - 打开 Visual Studio，转到“文件”>“新建”并选择“项目”。然后从对话框中选择一个新项目，选择“Windows 服务”，然后单击“确定”按钮。

- **步骤 2** - 转到 Visual C# -> “Windows 桌面” -> “Windows 服务”，输入合适的名称，然后单击“确定”。单击“确定”按钮后，服务界面会出现。

- **步骤 3** - 右键单击空白区域，选择“添加安装程序”。

**向 Windows 服务添加安装程序** - 在 Windows 服务能够运行之前，应安装安装程序，以便将其注册到服务控制管理器。添加安装程序后，ProjectInstaller 将添加到项目中，并且 ProjectInstaller.cs 文件将打开。现在可以保存所有内容。

- **步骤 4** - 右键单击空白区域，选择“查看代码”。

- **步骤 5** - 它有一个构造函数，其中包含 Initialize Component 方法。Initialize Component 方法包含创建并初始化拖放到窗体表面上的用户界面对象的逻辑，并提供窗体设计器的属性网格。需要注意的是，在调用 Initialize Component 方法之前，不应调用任何其他方法。

- **步骤 6** - 选择 InitializeComponent 方法，并按 F12 键转到定义

- **步骤 7** - 现在添加以下代码行，

```
this.serviceProcessInstaller1.Account
= System.ServiceProcess.ServiceAccount.LocalSystem;
```

可选地，可以如下所示添加描述和显示服务名称，

```
this.serviceInstaller1.Description = "First Service demo";
this.serviceInstaller1.DisplayName = "FirstService.Demo";
```

- **步骤 8** - 在此步骤中，设置一个计时器，并实现一段代码以在给定时间调用服务。可以为此创建一个文本文件，并使用该服务将当前时间添加到文本文件中。

### Service1.cs 类

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.IO;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.Threading.Tasks;
using System.Timers;
namespace FirstService {
public partial class Service1 : ServiceBase {
Timer timer = new Timer1(); // name space(using System.Timers;)
public Service1() {
InitializeComponent();
}
protected override void OnStart(string[] args) {
WriteToFile("Service is started at " + DateTime.Now);
timer.Elapsed += new ElapsedEventHandler(OnElapsedTime);
timer.Interval = 5000; //number in milliseconds
timer.Enabled = true;
}
protected override void OnStop() {
WriteToFile("Service is stopped at " + DateTime.Now);
}
private void OnElapsedTime(object source, ElapsedEventArgs e) {
WriteToFile("Service is recalled at " + DateTime.Now);
}
}
public void WriteToFile(string Message) {
    string path = AppDomain.CurrentDomain.BaseDirectory + "\\Logs";
    if (!Directory.Exists(path)) {
        Directory.CreateDirectory(path);
    }
    string filepath = AppDomain.CurrentDomain.BaseDirectory + "\\Logs\\ServiceLog_" + DateTime.Now.Date.ToShortDateString().Replace('/', '_') + ".txt";
    if (!File.Exists(filepath)) {
        // Create a file to write to.
        using(StreamWriter sw = File.CreateText(filepath)) {
            sw.WriteLine(Message);
        }
    } else {
        using(StreamWriter sw = File.AppendText(filepath)) {
            sw.WriteLine(Message);
        }
    }
}
```

代码说明 - 上述代码将每 5 秒调用一次服务，如果文件夹不存在则创建文件夹，并写入指定的消息。

- **步骤 9** - 通过右键单击项目或解决方案并选择“重新生成”来重新生成应用程序。

- **步骤 10** - 搜索“命令提示符”，并以管理员身份运行。

- **步骤 11** - 在命令提示符中执行以下命令，然后按 ENTER 键。

```
cd C:\Windows\Microsoft.NET\Framework\v4.0.30319
```

![](img/3005a4307e6d8f3bb7e76eea28a92357_827_0.png)

- **步骤 12** - 现在转到项目源文件夹 > bin > Debug，并复制 Windows 服务 exe 文件的完整路径。

### 安装 Windows 服务

打开命令提示符，执行以下命令，然后按 ENTER 键。

### 语法

```
InstallUtil.exe + service path + \ service name + .exe
```

检查 Windows 服务的状态

按以下步骤打开服务：

- 1. 按 Windows 键 + R。
- 2. 输入 services.msc
- 3. 查看正在运行的服务

### 检查 Windows 服务输出

该服务将创建一个包含以下文本的文本文件。

日志文件夹将在 bin 文件夹中创建。

### 卸载 Windows 服务

要卸载该服务，请使用以下命令，

```
InstallUtil.exe -u + service path + \service name + .exe
```

## 25.2 Windows Workflow Foundation (WF / WinWF)

### 25.2.1 WWF 简介

- Windows Workflow Foundation（WF 或 WinWF）是 Microsoft 的编程模型，用于在 Windows 操作系统中构建支持工作流的应用程序。
- WWF 提供了一个基于 .NET Framework 构建的平台，用于构建工作流。它不是一个应用程序或服务器产品，而是作为 .NET 3.0 Framework 的组件包含在内。该平台释放了一种完全不同范式的力量。WWF 为开发人员提供了一种声明式方式来为应用程序的“流”建模。WWF 还包括用于处理长时间运行工作流的 API，以及将设计器“重新承载”在自定义应用程序中的能力，从而在构建工作流时提供极大的灵活性。WWF 最初随 .NET 3.0 引入，并在 .NET 4 中进行了彻底改造。
- 工作流将生产过程建模为一组应用于进行中工作的活动。因此，随着工作从开始到完成在模型中推进，工作流描述了活动之间的执行顺序和依赖关系，而这些活动由人员或系统功能执行。

### 25.2.2 WWF - 基本概念与构建工作流

WWF 包括命名空间、工作流引擎和可与 Visual Studio .NET 一起使用的设计工具。WWF 涵盖系统工作流和人工工作流，并且可用于 Windows 的客户端和服务器版本。

### 25.2.2.1 工作流

在 WWF 术语中，**工作流** 就是 **完成特定任务所需的一系列步骤、决策和规则。**

**下面列出了工作流的一些主要标准，**

- 1. 流程的可视化表示
- 2. 可在运行时动态修改
- 3. 可长时间运行

**工作流主要有两种类型 -**

- 1. **顺序工作流 -** 用于定义良好的流程工作流。一系列活动按顺序调用。
- 2. **状态机工作流 -** 组织为状态机图，通常用于涉及人机交互的工作流。活动根据不同参数的“状态”进行调用。

- * 两种工作流解决方案都可以在 WWF 中创建，而且由于工作流是基于状态的，WWF 提供了良好的支持，例如，如果工作流到达某一状态后会在几分钟/几小时/几天/几个月内保持不变，那么它将被“持久化”，之后可以在任何不同的计算机/平台上轻松恢复，无需任何麻烦。此功能及许多其他功能都是 WWF 的一部分。
- * 工作流可以仅使用标记、仅使用代码，或同时使用标记和代码，以声明方式构建。
- * 工作流开发完成后，可以承载在任何能够加载工作流运行时的应用程序上，例如 Windows 窗体、Windows 服务、ASP.NET 网站和 Web 服务。

### 25.2.2.2 工作流运行时引擎

- * 每个正在运行的工作流实例都由进程内运行时引擎创建和维护，该引擎通常称为工作流运行时引擎。一个应用程序域内可以有多个工作流运行时引擎，并且运行时引擎的每个实例都可以支持多个并发运行的工作流实例。

