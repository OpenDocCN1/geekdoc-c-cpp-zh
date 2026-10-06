

# 附录

6. 在配置属性（Configuration Properties）下，展开链接器（Linker）节点。打开**附加依赖（Additional Dependencies）**旁边的组合框并输入 C:\Program Files\MySQL\MySQL Connector C 6.1.lib\libmysql.lib，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_398_0.png)

7. 使用 Windows 文件资源管理器，导航到 C:\Program Files\MySQL\MySQL Connector C 6.1.lib。将 mysql.dll 文件复制到 C:\Windows\System32。

现在，你可以编译并运行 **MultithreadedDBTest** 项目或任何使用 MySQL Connector/C 的项目。

# 安装 WinDK – 驱动程序开发包

为了使用 Windows 驱动程序包（WDK），你需要执行以下操作：

- 1. 打开浏览器并访问 http://msdn.microsoft.com/en-us/library/windows/hardware/hh852365.aspx。由于我们使用的是 Visual Studio 2013，你需要下载 WDK 8.1 或使用以下地址：
  http://go.microsoft.com/fwlink/link/p?LinkId=393659。以下是 WDK 下载页的截图：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_399_0.png)

- 2. 点击“下一步”并选择你是否愿意参与客户体验改进计划，然后接受许可协议以开始安装。你会看到如下所示的窗口：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_399_1.png)

- 3. 等待安装完成并关闭向导。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_400_0.png)

现在，Windows Driver程序包已成功安装。

# 设置用于驱动程序编译的 Visual Studio 项目

为了获得 Windows 驱动程序包的功能（如编译器和库），你需要设置 Visual Studio 项目属性。要执行此操作，请执行以下步骤：

- 1. 如果你遵循了第 2 章“线程概念（Thread Concept）——示例：在内核中实现线程”的说明，请打开解决方案 KernelThread。在解决方案管理器中，右键点击 DriverApp 并选择“属性”。在“常规”选项卡下，选择“目标扩展（Target Extension）”并点击“编辑”。将 .exe 重命名为 .sys。点击“应用”，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_401_0.png)

- 2. 展开 C++ 节点，并在“常规”下选择**附加目录（Additional Directories）**。点击**编辑**并输入以下路径：`C:\Program Files (x86)\Windows Kits\8.1\Include.km`。点击“确定”然后点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_401_1.png)

- 3. 现在，在 C++ 下移除所有“预处理器（Preprocessor）”，并在“预处理器定义（Preprocessor Definitions）”下选择“编辑”。删除所有行，如果激活了 Win32 配置，则输入 _x86_；如果激活了 x64 配置，则输入 _AMD64_，如下：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_402_0.png)

- 4. 点击确定并应用。现在，在“代码生成（Code Generation）”下，选择“启用 C++ 异常”并删除所有文本留空。点击“应用”。在“基本运行时检查（Basic Runtimes Check）”下，选择“默认”然后点击“应用”。在“安全检查（Security Check）”下，选择“禁用安全检查 (/GS-)”并点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_403_0.png)

- 5. 现在，在“高级（advanced）下，选择“调用约定（calling convention）”并如下选择 _stdcall (/Gz) ：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_403_1.png)

- 6. 现在，展开链接器节点，并在“常规”下，选择“启用增量链接（Enable Incremental Linking）”并选择“否 (INCREMENTAL:NO)”。现在，在“输入”下，选择“附加依赖 (x86)”并点击“编辑”。输入以下行：C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\ntoskrnl.lib 和 C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\hal.lib。注意根据你的解决方案配置将 x64 改为 x86：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_404_0.png)

- 7. 点击确定并选择应用。现在，展开“清单文件（Manifest File）”节点并选择“生成清单（Generate Manifest）”。从下拉列表中选择“否 (/MANIFEST:NO)”。点击“应用”。现在，展开“系统（System）”节点并选择“子系统（SubSystem）”。从下拉列表中选择“原生 (/SUBSYSTEM:NATIVE)”。选择“驱动程序（Driver）”并在下拉列表中选择“驱动程序 (Driver)”。点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_405_0.png)

- 8. 最后，选择**高级（Advanced）**节点并选择**入口（Entry Point）**。插入文本 `DriverEntry`。在**基地址（Base Address）**下插入文本 `x0`。然后选择**随机基地址（Randomize Base Address）**并删除所有文本留空。选择**数据执行防护（Data Execution Prevention）**并删除所有文本留空。选择“导入库（Import Library）”插入文本 `ntoskrnl.lib`。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_405_1.png)

现在，你可以编译并运行 DriverApp。注意，如果你使用的是 64 位操作系统，在修改“高级启动选项”之前，无法启动未数字签名的驱动程序；Vista 及更高版本的 Windows 支持 F8 高级启动选项，即“禁用签名强制（Disable Driver Signature Enforcement）”，这将禁用当前会话内核驱动程序的加载时签名强制。此设置在重启系统后失效（来自 MSDN）。更多信息请访问 http://microsoft.com/en-us/library/windows/hardware/ff57565(v=vs.85).aspx。

# 使用 DebugView 

为了显示驱动程序的输出，你需要使用 DebugView 。

- 1. 打开浏览器访问 http://technet.microsoft.com/en-us/internals/bb964.aspx。下载 DebugView ZIP 文件并解压到文件夹。运行 DebugView 程序，从菜单选择“捕获（Capture）”。勾选“内核（Kernel)”或按 Ctrl + K。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_406_0.png)

- 2. 现在，运行驱动程序，将在 DebugView 窗口中看到输出。

# 设置用于驱动程序的 Visual Studio 项目

为了获得 Windows 驱动程序包的功能（如编译器和库），你需要设置 Visual Studio 项目属性。要执行此操作，请执行以下步骤：

- 1. 如果你遵循了第 2 章“线程概念——示例：在内核中实现线程”的说明，请打开解决方案 KernelThread。在解决方案管理器中，右键点击 DriverApp 并选择“属性”。在“常规”选项卡下，选择“目标扩展（Target Extension）”并点击“编辑”。将 .exe 重命名为 .sys。点击“应用”，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_407_0.png)

- 2. 展开 C++ 节点，并在“常规”下选择**附加目录（Additional Directories）**。点击**编辑**并输入以下路径：`C:\Program Files (x86)\Windows Kits\8.1\Include.km`。点击**确定**然后点击**应用**。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_407_1.png)

- 3. 现在，在 C++ 下移除所有“预处理器（Preprocessor）”，并在“预处理器定义（Preprocessor Definitions）”下选择“编辑”。删除所有行，如果激活了 Win32 配置，则输入 _x86_；如果激活了 x64 配置，则输入 _AMD64_，如下：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_408_0.png)

- 4. 点击确定并应用。现在，在“代码生成（Code Generation）”下，选择“启用 C++ 异常”并删除所有文本留空。点击“应用”。在“基本运行时检查（Basic Runtimes Check）”下，选择“默认”然后点击“应用”。在“安全检查（Security Check）”下，选择“禁用安全检查 (/GS-)”并点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_409_0.png)

- 5. 现在，在“高级（advanced）下，选择“调用约定（calling convention）”并如下选择 _stdcall (/Gz) ：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_409_1.png)

- 6. 现在，展开链接器节点，并在“常规”下，选择“启用增量链接（Enable Incremental Linking）”并选择“否 (INCREMENTAL:NO)”。现在，在“输入”下，选择“附加依赖 (x86)”并点击“编辑”。输入以下行：C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\ntoskrnl.lib 和 C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\hal.lib。注意根据你的解决方案配置将 x64 改为 x86：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_410_0.png)

- 7. 点击确定并选择应用。现在，展开“清单文件（Manifest File）”节点并选择“生成清单（Generate Manifest）”。从下拉列表中选择“否 (/MANIFEST:NO)”。点击“应用”。现在，展开“系统（System）”节点并选择“子系统（SubSystem）”。从下拉列表中选择“原生 (/SUBSYSTEM:NATIVE)”。选择“驱动程序（Driver）”并在下拉列表中选择“驱动程序 (Driver)”。点击“应用”。

- 8. 最后，选择**高级（Advanced）**节点并选择**入口（Entry Point）**。插入文本 `DriverEntry`。在**基地址（Base Address）**下插入文本 `x0`。然后选择**随机基地址（Randomize Base Address）**并删除所有文本留空。然后选择**数据执行防护（Data Execution Prevention）**并删除所有文本留空。选择“导入库（Import Library）”插入文本 `ntoskrnl.lib`。

现在，你可以编译并运行 DriverApp。注意，如果你使用的是 64 位操作系统，在修改“高级启动选项”之前，无法启动未数字签名的驱动程序；Vista 及更高版本的 Windows 支持 F8 高级启动选项，即“禁用签名强制（Disable Driver Signature Enforcement）”，这将禁用当前会话内核驱动程序的加载时签名强制。此设置在重启系统后失效（来自 MSDN）。

