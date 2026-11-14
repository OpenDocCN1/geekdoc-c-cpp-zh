

你的应用程序。这些示例可以作为学习 Electron.NET 的一个良好起点。在我们可以详细审查的技术中，有原生菜单和原生对话框窗口。

- 使用原生个性化菜单（需要特定控制器，MVC）。

你可以在下方看到一段用于在项目中实现原生菜单的代码片段（MVC 控制器）。

```
public class MenusController : Controller
{
    public IActionResult Index()
    {
        if (HybridSupport.IsElectronActive)
        {
            var menu = new MenuItem[] {
                new MenuItem { Label = "Edit", Submenu = new MenuItem[] {
                    new MenuItem { Label = "Undo", Accelerator = "CmdOrCtrl+Z", Role = MenuRole.undo },
                    new MenuItem { Label = "Redo", Accelerator = "Shift+CmdOrCtrl+Z", Role = MenuRole.redo },
                    new MenuItem { Type = MenuType.separator },
                    new MenuItem { Label = "Cut", Accelerator = "CmdOrCtrl+X", Role = MenuRole.cut },
                    new MenuItem { Label = "Copy", Accelerator = "CmdOrCtrl+C", Role = MenuRole.copy },
                    new MenuItem { Label = "Paste", Accelerator = "CmdOrCtrl+V", Role = MenuRole.paste }
                } }
            };
            Electron.Menu.SetApplicationMenu(menu);
        }
        return Ok();
    }
}
```

这只是一个示例代码片段，用于说明在应用程序中实现原生菜单的方法，你应该考虑详细审查工作示例代码中是如何实现的（查看项目中 menu.cs 文件的源代码以获取实际示例）。

- 本示例中还审查了消息对话框窗口的使用（此技术也用于 FileOpen、FileSave 和错误消息对话框窗口）。

由于 Electron.NET 应用程序底层运行着两个进程，因此有两段不同的代码（片段）用于实现平台原生菜单：一段用于渲染部分（HTML/JavaScript），另一段用于后端应用程序（C# 进程）。

以下是创建原生消息窗口的代码片段（JavaScript）。

```
document.getElementById("information-dialog").addEventListener("click", () => {
    ipcRenderer.send("information-dialog");
});
ipcRenderer.on("information-dialog-reply", (sender, index) => {
    let message = 'You selected ';
    if (index == 0) {
        message += 'yes.';
    } else {
        message += 'no.';
    }
});
document.getElementById("info-selection").innerText = message;
});
```

以及要包含在 C# 后端中的代码。

```
Electron.IpcMain.On("information-dialog", async (args) => {
    var options = new MessageBoxOptions("This is an information dialog. Isn't it nice?")
    Type = MessageBoxType.info,
    Title = "Information",
    Buttons = new string[] { "Yes", "No" }
});

var result = await Electron.Dialog.ShowMessageBoxAsync(options);

var mainWindow = Electron.WindowManager.BrowserWindows.First();
Electron.IpcMain.Send(mainWindow, "information-dialog-reply", result.Response);
});
```

有多种可用的原生对话框窗口类型（除了上面描述的那种之外），你可以详细审查 dialog.cs 文件的代码，以获取更多关于如何使用此功能的示例。

这只是示例应用程序中展示的少数功能之一，但从 Web 应用程序开发者的角度来看，它们似乎是最特别的部分。

如你所见，应用程序中这些基本功能（菜单和对话框）的实现并不明显。管理 Electron 架构引入的双进程存在很多复杂性。随着应用程序本身变得更加复杂，这种复杂性也会增加。

研究“ElectronNET-API-Demos”项目可以在 Electron.NET 开发所需的学习阶段为你提供帮助。

**注意：** 此示例无法从 Visual Studio 2019 IDE 执行，在这种情况下，你必须使用“dotnet CLI”。

“ElectronNET-API-Demos”的完整源代码可在 GitHub 上获取。

![](img/3d310cc066dda6e2dfa67a650614076f_161_0.png)

请注意，Electron.NET 仍在持续开发中，它对应用程序中包含的每个包的版本非常敏感。这使得构建过程变得有些不可靠，当你尝试使用互联网上的代码示例应用程序（旧版本）时。

你可以在下方查看应用程序在各平台上的渲染效果。

## 在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_162_0.png)

## 在 Ubuntu 上：

- ELECTRON.NET API 演示
- 网络
- 云管理器 Windows
- 启动 Windows 任务栏和日志
- API
- 云管理器 Windows
- 云管理器 Windows
- 在系统文件管理器中打开外部链接
- 关于何时发生情况的指示...
- 显示进度
- 显示进度
- 配置
- 编译 Electron.NET API 演示
- 演示
- 打开系统信息
- 从此剪贴板创建和打印
- 数据包 PING
- 截图

## 使用系统对话框

Electron.NET API 演示允许你使用系统对话框来打开文件、打印文件、启动文件或编辑信息消息。

这更原生、更易用，因为使用原生回调的过程更有效，并允许在进程间远程调用。请参阅 electron.net 页面的渲染进程。

![](img/3d310cc066dda6e2dfa67a650614076f_163_0.png)

## 错误对话框

错误：ELECTRON.NET / API / DEMOS / API / DEMOS

## 信息对话框

ELECTRON.NET / API / DEMOS / API / DEMOS

查看演示

在此演示中，Electron.NET API 将向渲染进程发送一条消息以打开信息对话框。渲染进程将捕获该消息并执行响应，随后该响应可以反映回渲染进程。

注意：Electron.NET 属性在 macOS 上被禁用。

信息对话框可以包含图标、你选择的按钮、标题和消息。

## 在 Windows 上：

- 文件
- 编辑
- 视图
- 窗口
- 帮助

## 试玩

在你自己的 Electron 应用中使用演示小程序。Electron 快速入门应用是一个精简应用，可与这些演示一起使用。按照此处的说明开始并克隆 Electron 快速入门。将 Electron.NET API 演示用作你的 ASP.NET Core API。

## 构建 Electron.NET 快速入门

这包括将 ElectronNET.WebHostExtensions 扩展包含在你的 ASP.NET Core 项目的 Program.cs 文件中。

```
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
    .UseElectron(args)
    .UseStartup<Startup>()
    .Build();
```

![](img/3d310cc066dda6e2dfa67a650614076f_163_1.png)

当你在 Windows 上运行应用程序时（使用“dotnet electronize start”命令），安全对话框窗口通常会出现（取决于使用的安全级别），你必须确认所提议的安全规则（在下方窗口中单击“确定”）。

![](img/3d310cc066dda6e2dfa67a650614076f_164_0.png)

## 8.3.6 Electron.NET 应用程序的优缺点

由于这是一种 Web GUI 实现，因此应用程序在每个平台上的渲染效果非常相似。跨平台的 GUI 显示一致性是此类解决方案实现的特征（及优势）之一。使用增强型 JavaScript 界面设计的能力是另一个优势，但此类桌面应用程序的性能并不总是最佳。

即使你可以使用 Visual Studio 开发工具来开发 Web 应用程序部分，Electron.NET 工具也无法在 Visual Studio 2019 内使用，你必须使用“dotnet CLI”来初始化、运行、构建和打包应用程序（如前所述）。

Electron.NET 为 ASP.NET 开发者提供了将其应用程序作为离线桌面环境执行的目标的能力，尽管如此，在这样做之前，需要掌握一些特定的 Electron.NET 知识。即使你是一位资深的 ASP.NET Web 开发者，你也必须经历一个学习曲线来掌握桌面开发的特定要求。

注意：Electron.NET 的版本对你必须使用的 .NET Core 版本非常严格，你必须找到 Electron.NET 版本和 .NET Core 版本的正确组合才能构建和执行程序（在某些情况下可能比较棘手）。

## 8.4 C++ 原生 GUI 应用程序

在 .NET Core 3 应用程序中实现原生 UI 有几种解决方案。使用原生 GUI 可以让每个操作系统的用户感觉该应用程序是专为其平台开发的。通过使用标准表单和控件，用户可以直接熟悉软件界面（应用程序看起来像原生应用）。

三个系统（Linux、macOS、Windows）上图形基元的稳定标准化，为开发者提供了编写可在每个系统上运行的图形界面的机会。通过使用适配的包装器，.NET Core 3 开发者

