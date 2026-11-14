

Electron.NET.CLI 是用于构建和打包 Electron 应用程序的命令行工具，它不用于应用程序的代码内部（它是一个工具）。Electron.NET.CLI 对于运行你的 .NET Core Electron.NET 应用程序是必需的。

你可以使用下面描述的命令行安装此工具（这是 dotnet CLI 的工具集包）。它可以作为 dotnet CLI 的全局工具安装，通过“electronize”命令扩展它。

```
C:> dotnet tool install ElectronNET.CLI -g
```

在 .NET Core 中设置 Electron.NET.CLI 后，“electronize”命令可作为 dotnet CLI 的全局工具使用。“electronize”命令仅针对特定的 .NET Core 版本安装，该工具本身安装在用户文件夹中：%UserProfile%/.dotnet/tool/

但在使用 Electron.NET 包装器之前，.NET Core 应用程序开发者必须安装先决条件工具：Node.JS 及其依赖项 NPM。

## 8.3.3 NPM 和 Node.JS 的设置

NPM 代表 Node Package Manager，Node.JS 是来自 Chromium 项目（由 Google 开发）的 JavaScript 运行时引擎。Electron.NET 要求 Node.JS 版本 >8.6。我们建议从专用网站安装 NodeJS（参考中提供了网址），以获取工具的最新版本并确保在每个系统上正确安装。

以下是下载安装文件的参考链接（以及获取此处审查的每个操作系统的文档）。

https://www.npmjs.com/get-npm
https://nodejs.org/en

我们将详细介绍如何在每个平台上安装这些工具，因为这是使用 Electron 框架的核心要求，并且常常在项目构建过程中构成问题。

### 8.3.3.1 在 macOS 上

对于此平台，我们建议安装 Node.js 网站上的版本（这是最新版本，在构建 Electron.NET 应用程序时不应该出现版本号问题）。

下载后，你需要通过点击它来安装该工具（这是一个 .pkg 文件）。产品安装成功后，你应该看到如下界面

![](img/3d310cc066dda6e2dfa67a650614076f_151_0.png)

安装过程完成后，我们建议在开始构建 Electron.NET 应用程序之前重启计算机（以确保每个环境变量都已更新）。

### 8.3.3.2 在 Ubuntu 上

在 Linux 系统上，你可以使用通常的包管理器“apt”通过以下命令安装 Node.JS，你还需要安装 NPM，因为它不在这个环境的同一包中。

```
$ sudo apt-get update
$ sudo apt-get install nodejs
$ sudo apt-get install npm
```

成功安装的样子如下。

```
File Edit View Search Terminal Help
johngubuntu:~$
Get:1 http://us.archive.ubuntu.com/ubuntu bionic/main amd64 libhttp-parser2.7.1
amd64 2.7.1-1build1 [39.8 kB]
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 nodejs amd64 8.10.0.dfsg-2ubuntu0.4 [4.790 kB]
Fetched 5,058 kB in 47s (102 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
libhttp-parser2.7.1
Preparing to unpack .../libhttp-parser2.7.1_2.7.1-1build1_amd64.deb ...
Unpacking libhttp-parser2.7.1 (2.7.1-1build1) ...
Setting up libhttp-parser2.7.1 (2.7.1-1build1) ...
Preparing to unpack .../nodejs_8.10.0.dfsg-2ubuntu0.4_amd64.deb ...
Unpacking nodejs (8.10.0.dfsg-2ubuntu0.4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Setting up nodejs (8.10.0.dfsg-2ubuntu0.4) ...
update-alternatives: using /usr/bin/nodejs to provide /usr/bin/js (js) in auto mode
Processing triggers for libc-bin (2.27-3ubuntu1) ...
root@ubuntu:~#
```

一旦两个包都已正确（无错误）安装，你可以使用以下命令控制已安装的版本。

```
$ nodejs -v
```

使用此命令还可以帮助你验证一切是否正常运行（验证安装是否正确执行）。显示的版本号必须 >8.6。

### 8.3.3.3 在 Windows 上

在 Windows 上，你必须安装 NPM 和 Node.js。
Visual Studio Installer 程序中的 Node.JS 版本设置不适用于构建 Electron.NET 应用程序（因为你还需要安装 NPM）。我们建议不要为这项特定任务使用此版本。

更简单的解决方案是从专用网站设置 Node.JS/NPM，这将确保你安装最新可用版本（链接已在前面的参考中提供）。

以下是安装程序的界面。

![](img/3d310cc066dda6e2dfa67a650614076f_153_0.png)

Windows 要求你在开始使用之前重启系统，以使用新的环境变量更新系统。

## 8.3.4 Electron.NET 快速入门

使用 Electron.NET 意味着需要遵循一个过程，以便将其集成到 ASP.NET Core 应用程序中并将其转换为桌面应用程序。

以下是“electronize”你的 ASP.NET Core 3 应用程序的简短过程。我们将在后面更详细地审查应用程序代码本身（在示例部分中）。

- A) 创建 ASP.NET Core MVC 应用程序

可以使用 dotnet CLI 或 Visual Studio 完成。

- B) 安装 Electron.NET 命令行全局工具（自版本 0.9 起）

在开始开发应用程序之前，你必须使用下面描述的命令行安装 dotnet CLI 的 Electron.NET.CLI 全局工具。

```
$ dotnet tool install --global Electron.NET
```

- C) 添加 Electron.NET 包：

除了从 Visual Studio NuGet 包管理器添加它之外，你还可以在包管理器命令行中键入以下行来添加依赖项。

```
PM> Install-Package Electron.NET.API
```

### D) 设置打包（仅适用于 ubuntu 和 macOS）

此步骤仅适用于 ubuntu 和 macOS 平台，在这些操作系统上，你需要使用以下命令行指令安装“electron-builder”。

```
$ sudo npm install electron-builder --global
```

### E) 开始使用 Electron.NET：

你可以通过在 WebHostBuilder 中使用以下代码来实现这一点。

```
public static IWebHost BuildWebHost(string[] args)
{
    return WebHost.CreateDefaultBuilder(args)
        .UseElectron(args)
        .UseStartup<Startup>()
        .Build();
}
```

你可以注意到，我们刚刚将“UseElectron(args)”行添加到了 WebHost 中，以便在 MVC ASP.NET Core 应用程序中启用 Electron 的使用。

### F) 在 Startup.cs 文件中创建 Electron 窗口：

这可以通过在“Configure”方法中使用以下指令来完成：

```
Task.Run(async () => await Electron.WindowManager.CreateWindowAsync());
```

使用这行代码，Web 应用程序在 Electron 窗口中执行。

### G) 应用程序初始化：

第一次启动 Electron 应用程序时，你必须使用下面描述的命令对其进行“初始化”（你必须位于应用程序文件夹中）。

```
::\appPath>dotnet electronize init
```

此命令将创建“electron.manifest.json”文件，该文件由“electronize”命令用于程序的执行（此文件描述 Electron 上下文）。

### H) 执行应用程序：

之后，你可以使用“start”命令执行 Electron.NET ASP.NET Core 应用程序，如下面描述（在 Windows 上位于应用程序文件夹中，在 ubuntu 和 macOS 上位于解决方案文件夹中）。

```
::\appPath>dotnet electronize start
```

在 ubuntu 和 macOS 上，你必须使用不带“dotnet”部分的“electronize”命令，如下面描述。

```
> electronize start
```

使用此命令，应用程序在经典桌面应用程序窗口中执行（不在浏览器中，但这仍然是一个 Web 应用程序）。

## 8.3.5 Electron.NET 应用程序示例

由于 Electron.NET 是围绕 Electron 的流行包装器，你将找到大量代码示例（查看 GitHub）来帮助和指导你开发 Electron.NET 应用程序（请参阅参考链接）。

这些示例通常大量使用 SPA（单页应用程序）技术，并使用 Vue.JS 或 React 等专业 JavaScript 框架……原因是桌面应用程序体验需要最小限度的屏幕闪烁，以便用户喜欢并看起来像一个实体桌面应用程序。

因此，使用 Electron.NET 开发应用程序意味着大量使用 JavaScript 来在 Web 开发后端和桌面前端之间创建缓冲（桌面前端自然倾向于像普通 Web 应用程序一样闪烁）。

我们将审查的 Electron.NET、ASP.NET Core 示例应用程序是 Electron.NET 仓库中的“ElectronNET-API-Demos”应用程序。

这是此类应用程序的参考应用程序。它说明了许多 Electron.NET 功能的使用。大部分源代码在应用程序本身中公开，用于教学目的。

在此示例中，你将找到一些特定于 Electron.NET 应用程序类型的有用技术，这些技术可以重复用于

