

# 第 XII 部分：MAXScript 和插件

## 绝对变换赋值
这告诉宏记录器，你所做的任何变换都不是相对于对象的当前位置或方向的。例如，如果你将一个球体从 (0,0,0) 移动到 (10,0,0)，宏记录器会编写 MAXScript 说：“将对象移动到 (10,0,0)。”

## 相对变换操作
使用此选项可使宏记录器相对于对象的当前状态应用变换。例如，如果你将一个球体从 (0,0,0) 移动到 (10,0,0)，宏记录器会说：“将对象从其当前位置沿 X 方向移动 +10 个单位。”

## 显式子对象集
如果你选择此选项然后记录一个操作子对象集的脚本，重新运行脚本时始终会操作那些相同的子对象，即使你在再次运行脚本时选择了其他子对象。

## 相对于选择的的子对象集
这告诉宏记录器，你希望脚本在运行脚本时操作所选的任何子对象。

## 显示命令面板切换
此选项告诉宏记录器是否要为在命令面板上进行的操作编写 MAXScript。

## 显示工具选择
如果选择此选项，宏记录器会记录更改为不同工具的 MAXScript。

## 显示菜单项选择
此选项告诉宏记录器是否希望它为你在记录脚本时选择的菜单项生成 MAXScript。

# 教程：记录一个简单的脚本

在本教程中，你将创建一个简单的脚本，该脚本会压扁你所选的任何对象并将其变成紫色。

要使用宏记录器创建脚本，请按照以下步骤操作：

- 1. 打开 DVD 上第 49 章目录中的 Purple pyramid.max 文件。此文件包含一个简单的金字塔对象。
- 2. 在选择金字塔对象后，选择 MAXScript ⇨ MAXScript Listener（或按 F11）打开 MAXScript Listener 窗口。
- 3. 在 Listener 窗口中，打开 MacroRecorder 菜单并确保所有选项都设置为相对而不是绝对对象设置，从而告诉脚本在任何所选对象上工作，而不是始终修改同一个对象。
- 4. 返回到 MacroRecorder 菜单，选择 Enable。宏记录器现在已打开并准备开始编写 MAXScript。最小化宏记录器窗口（或至少将其移开，以便可以看到其他视口）。
- 5. 通过右键单击视口名称并选择 Views ⇨ Extended ⇨ MAXScript Listener，将 MAXScript Listener 窗口停靠到左侧视口。现在你可以在工作时保持界面整洁。
- 6. 在选择 Pyramid01 对象后，选择 Modifiers ⇨ Parametric Deformers ⇨ XForm 为对象添加 XForm 修改器。
- 7. 选择非均匀缩放工具并将其限制在 Y 轴。右键单击正面视口中的任意位置使其处于活动状态（如果尚未处于活动状态），然后向下拖动 Y 轴 gizmo 以压扁金字塔。
- 8. 在 Modify 面板中，单击对象名称字段旁边的颜色样本以打开 Object Color 对话框。选择其中一种紫色，然后单击 OK。
- 9. 脚本已完成，因此在 MAXScript Listener 窗口中，选择 MacroRecorder ▸ Enable 以关闭宏记录器。
- 10. 现在是尝试你的第一个 MAXScript 作品的时候了。将一个球体添加到你的场景中。在进入下一步之前确保它已被选中。
- 11. 在 MAXScript Listener 窗口的顶部窗格中，选择所有文本（一种简便的方法是按 Ctrl+A），然后按住 Shift 键并按 Enter 键，告诉 Max 执行 MAXScript

在图 49.8 中，你可以看到脚本以及已被压扁并改变颜色的球体。

# 图 49.8

运行新的压扁并变紫脚本

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1232_0.png)

# MAXScript 调试器

MAXScript 调试器，如图 49.9 所示，是一个单独的窗口，允许你使用断点停止脚本的执行，并在脚本运行时查看变量的值。此信息提供了宝贵的信息，可帮助识别脚本中的错误。

MAXScript 调试器对话框是通过各种 MAXScript 工具窗口中的 Debugger 菜单命令或主界面上的 MAXScript ▸ Debugger Dialog 菜单命令打开的。调试器窗口顶部的 Command 字段允许你直接向调试器输入命令。Output 区域显示结果。调试器窗口底部的几个按钮可让你控制调试器的工作方式：

- **Break:** 导致当前脚本中断其执行
- **Run:** 启动当前脚本的执行
- **Evaluate:** 执行输入到 Command 字段中的命令
- **Watch:** 打开 Watch Manager 窗口，在其中你可以指定要监视的特定变量
- **Config:** 打开 MAXScript Debugger Parameters 对话框，在其中你可以配置调试器
- **Stop:** 中止当前脚本的执行
- **Clear:** 清除 Output 字段中的所有文本

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1233_0.png)

**图 49.9**  
MAXScript 调试器让你在脚本运行时检查变量的值。

# 监视变量

Watch 按钮打开 Watch Manager，如图 49.10 所示。单击 Variable 列即可输入要监视的新变量。Value 列在脚本执行时显示所列变量的值。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1233_1.png)

**图 49.10**  
Watch Manager 让你监视特定变量的值。

# 使用调试器命令

一旦通过单击 Break 按钮使脚本的执行被挂起，你就可以在调试器顶部的 Command 字段中输入特定命令并单击 Evaluate 按钮来执行它们。表 49.1 列出了可用的调试器命令。

# 表 49.1

# MAXScript 调试器命令

| Command | What It Does |
|---|---|
| threads | Displays a list of all current threads. |
| setThread (thread no.) | Makes the specified thread number the active thread. |
| stack | Dumps the stack for the active thread. |
| setFrame (frame no.) | Makes the specified frame number the active frame. |
| locals (variable) | Dumps the value for the specified variable for the active thread and frame. If no variable is listed, then all variable values are dumped. |
| getVar (variable) | Gets the value of the specified variable. |
| setVar (variable) | Sets the value of the specified variable. |
| eval (expression) | Evaluates the specified expression. |
| ? | Displays a list of debugger commands. |

# 配置调试器

Config 按钮打开 MAXScript Debugger Parameters 对话框，如图 49.11 所示。此对话框包含多个选项，用于决定何时中断脚本执行。它还让你定义每次中断的时间。

# 图 49.11

MAXScript Debugger Parameters 让你设置中断周期时间等设置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1234_0.png)

# 设置 MAXScript 首选项

Preference Settings 对话框，通过 Customize > Preference Settings 菜单命令打开，包含 MAXScript 设置面板，如图 49.12 所示。使用这些设置，你可以设置自动加载哪些脚本、宏记录器的默认设置，甚至 Script Editor 窗口中显示的字体。Use Fast Node Name Lookup 选项会导致所有索引的 MAXScript 名称保存在缓存缓冲区中以加快脚本的执行。

Max 在其默认安装中包含两个可用于在 Max 启动时自动加载脚本的目录。这些目录是 scripts 和 scripts\\startup，但你可以使用 Configure Paths 对话框更改它们。Load Startup Scripts 选项会导致在 Max 启动时自动加载这些目录中的任何脚本。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1235_0.png)

Preference Settings 对话框中的 MAXScript 面板包含用于控制 MAXScript 的选项。

# 脚本类型

并非所有脚本都一样，Max 根据它们的工作方式对不同脚本进行分类。有关更多信息，MAXScript 在线帮助提供了有关其各种选项的详尽信息。

在决定要创建何种类型的脚本时，主要考虑的是用户界面。问问自己对于你正在创建的工具类型，最合乎逻辑的用户界面是什么，这可以提示你哪种类型的脚本适合该任务。

# 宏脚本

宏脚本是使用宏记录器创建的脚本。任何与工具栏按钮关联的脚本都被视为宏脚本。Max 按其类别组织宏脚本，你可以通过编辑脚本文件来更改它。要从另一个脚本调用宏脚本，可以使用 macros 命令。例如，

```
macros.run "objects" "sphere"
```

运行“objects”类别中的“sphere”脚本。

宏脚本通常不需要其他用户输入；你只需单击按钮，脚本就会发挥其魔力。

