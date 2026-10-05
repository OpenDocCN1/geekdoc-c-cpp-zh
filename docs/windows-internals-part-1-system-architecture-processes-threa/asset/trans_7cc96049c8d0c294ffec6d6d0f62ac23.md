

Windows 会请求远程用户的用户标识。在加入域的系统中，Windows 会通过请求用户的管理员身份来尊重用户所有的组成员身份。执行请求管理权限的映像会导致应用程序信息服务（AIS，包含在 %SystemRoot%\System32\Appinfo.dll 中，它运行在标准的服务宿主进程（Svchost.exe）内部）启动 `%SystemRoot%\System32\Consent.exe`。Consent 会捕获屏幕的位图，应用淡入效果，切换到仅限本地账户访问的桌面（安全桌面），将位图绘制为背景，并显示一个包含该可执行文件信息的提升对话框。此位于独立桌面的对话框可以防止用户账户中呈现的任何应用程序修改对话框的外观。

如果映像具有 Windows 组件的数字签名（由微软或其他实体签名），对话框顶部会显示一条浅蓝色条纹，如图 7-26 左侧所示（Windows 10 中已删除了微软签名镜像与其他签名者之间的区别）。如果镜像未签名，条纹将变为黄色，且提示会强调镜像的来源未知（见图 7-26 右侧）。对于数字签名的镜像，提升对话框会显示镜像的图标、描述和发布者；但对于未签名的镜像，仅显示名称和“发布者：未知”。这种差异使得恶意软件难以模仿合法软件的外观。对话框底部的“显示更多详细”（Show More Details）链接展开后显示如果启动时将执行的命令行。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_746_0.png)

图 7-26 基于镜像签名的 AAC UAC 提升对话框。

图 7-27 所示的 OTS 同意对话框类似，但会提示管理员凭据。它将列出所有具有管理员权限的账户。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_746_1.png)

图 7-27 OTS 同意对话框。

如果用户拒绝提升，Windows 会向进程启动返回拒绝访问错误。当用户通过输入管理员凭据或点击“是”同意提升时，AIS 会调用 `CreateProcessAsUser` 以适当的管理员身份启动进程。AIS 在技术上是提升进程的父进程；AIS 使用 `CreateProcessAsUser` API 的新支持，将父进程的进程 ID 设置为最初启动它的进程的 ID。这就是为什么提升后的进程不会出现在 Process Explorer 等显示进程树的 AIS 服务宿主工具图表中。图 7-28 显示了从标准用户账户启动提升进程涉及的操作。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_747_0.png)

**图 7-28** 以标准用户身份运行管理员应用程序。

## 请求管理员权限

系统和应用程序有多种方法识别对管理员权限的需求。出现在 Explorer 界面中的是“以管理员身份运行”（Run as Administrator）右键命令和快捷选项。这些项目还包含一个蓝金色的盾牌图标，它应该放置在任何选择后会导致权限提升的按钮或菜单项旁边。选择“以管理员身份运行”命令会导致 Explorer 调用带有运行动词的 `ShellExecute` API。

绝大多数安装程序都需要管理员权限，因此启动可执行文件启动的映像加载器包含了安装程序检测代码以识别旧版安装程序。它使用的一些启发式方法仅如检测内部版本信息，或者名称中是否包含“install”或“update”字样。更复杂的检测方法涉及扫描第三方安装封装器中常见的字节序列。映像加载器还会调用应用程序兼容性库查看目标可执行文件是否需要管理员权限。该库在应用程序兼容性数据库中查找可执行文件是否关联了 `ReqAdministrator` 或 `RunAsInvoker` 标记。

可执行文件请求管理员权限的最常见方法是其在清单文件中包含一个 `requestedExecutionLevel` 标签。该属性可以具有表 7-17 所示的三个值之一。

| 提升级别 | 含义 | 用途 |
| :--- | :--- | :--- |
| invoker | 不需要提升；永不请求提升。 | 典型应用程序 |
| highestAvailable | 请求批准；如果用户是标准用户，将出现 UAC 提示。 | 需要管理员权限的应用程序 |
| requireAdministrator | 始终请求管理员权限；如果用户以标准用户登录，将显示 UAC 提示。 | 需要管理员权限的应用程序 |

清单文件中 `trustInfo` 元素的存在（你可以在 eventwr.exe 的转储中看到）表示该可执行文件是使用 UAC 编写的，而 `uiAccess` 属性是辅助功能应用程序使用它的地方。

```
sigcheck -m C:\Windows\eventwr.exe
<trustInfo xmlns="urn:schemas-com:asmv3">
  <security>
    <requestedPrivileges>
      <requestedExecutionLevel
        level="highestAvailable"
        uiAccess="false"/>
    </requestedPrivileges>
  </security>
</trustInfo>
<asmv3:application>
  <asmv3:windowsSettings xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
    <asmv3:autoElevate>true</autoElevate>
  </asmv3:windowsSettings>
</asmv3:application>
```

## 自动提升

在默认配置下，下一节中的程序和控制面板不会产生提升提示，即使它们需要管理员权限。这是因为有一种被称为自动提升的机制。自动提升的目的是防止管理员用户在执行大部分工作时看到提升提示；它有几项要求。其中一项是程序必须被视为 Windows 可执行文件。这意味着它必须由 Windows 发布者签名（而不是微软——Windows 签名被认为权限更高）。它还位于几个安全目录之一：%SystemRoot%\System32 及其大部分子目录、%SystemRoot%\Home 以及 %ProgramFiles% 下的少量目录（例如包含 Windows Defender 和 Windows Journals 的目录）。

额外的要求取决于可执行文件的类型。除 mm.exe 以外的 EXE 文件通过清单中的 `autoElevate` 元素请求，则可以自动提升。前一节中 eventnr.exe 的清单就说明了这一点。

最后，COM（进程外服务器）可以在其注册表项中请求管理员权限。这需要一个名为 `Elevation` 的子项以及一个名为 `Enabled` 的 DWORD 值。COM 类及其实例化可执行文件都必须满足 Windows 可执行文件的要求，尽管可执行文件未请求自动提升。

## 控制 UAC 行为

UAC 可以通过图 7-29 所示的对话框进行修改。该对话框位于“用户账户控制设置设置。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_749_0.png)

图 7-29 用户账户控制设置对话框。

四个可能的设置的效果如表 7-18 所示。

第三个位置不建议使用，因为 UAC 提升提示不会出现在安全桌面上，而是出现在普通用户的桌面上。这允许在同一会话中运行的恶意程序更改提示的外观。它旨在视频系统变暗桌面时间过长或不适用于通常 UAC 显示的系统。

