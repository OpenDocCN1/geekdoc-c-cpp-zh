
`inputTextBox.Font = new (inputTextBox.Font.Family,`

`inputTextBox.Font.SizePoints+1);`

```
```

这会将 `TextBox` 的 `Font` 更改为使用 `TextBox` 当前字体的新对象，但通过增加 `SizePoints` 属性来增大字体大小。可以使用类似的方法减小字体。在多小的字号下，你能注意到这些孔呢？

**14.11** （项目：打字练习——计算机的关键技能）快速准确地打字是一项基本技能。在这个练习中，你将构建一个允许用户在不看键盘的情况下打字的应用。应用程序应显示用户输入的内容。应用程序应在屏幕上显示键盘并突出显示按下的按键。应用程序还应显示一个字数计数器。用户可以随时重置计数器。用户还可以更改文本颜色。用户还可以更改文本字体大小。用户能够将文本保存到文件中。

## 15.2 菜单

| 菜单项 | 子菜单 | 已用命令 | 视图 | 调试 | 工具 | 测试 | 分析 | 窗口 | 帮助 | | | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 解决方案管理器 | Ctrl+W, S | | | | | 连接... | | | 新窗口 |
| 团队管理器 | Ctrl+Alt, M | | | | | | | | 分割 |
| 服务器管理器 | Ctrl+W, L | | | | | | | | 浮动 |
| 云管理器 | Ctrl+Shift+X | | | | | | | | 停靠 |
| SQL Server 对象管理器 | | | | | | | | | 自动隐藏 |
| 编译窗口 | Ctrl+Shift+B | | | | | | | | | |
| 调用层次结构 | Ctrl+W, X | | | | | | | | 固定标签页 |
| 类树 | | | | | | | | | | 保存窗口布局 |
| 代码窗口 | Ctrl+Shift+D | | | | | | | | 应用窗口布局 |
| 对象浏览器 | Ctrl+W, J | | | | | | | | | 管理窗口布局 |
| 错误列表 | | | | | | | | | | 重置窗口布局 |
| 开始页 | | | | | | | | | | 自动模式 |
| 任务列表 | Ctrl+W, T | | | | | | | | | 关闭所有文档 |
| 通知 | Ctrl+W, X | | | | | | | | | 1 表[1] 设计 |
| 其他窗口 | | | | | | | | | | 窗口... |
| 工具栏 | | | | | | | | | | | | |
| 全屏 | Shift+Alt+Enter | | | | | | | | | | | |
| 浏览器导航 | Shift+Alt+Left | | | | | | | | | | | |
| 向进 | Shift+Alt+Right | | | | | | | | | | | |
| 下一个任务 | | | | | | | | | | | | |
| 上一个任务 | | | | | | | | | | | | |
| 属性窗口 | Ctrl+W, P | | | | | | | | | | | | |
| 页 | Shift+F4 | | | | | | | | | | | | |

![](img/57baed2319be0bb1b5f98674846f2711_639_0.png)

选中的菜单项分隔线

图 15.1 | 菜单、子菜单和菜单项。

要创建一个菜单，请使用工具箱并拖入 `MenuStrip`，这会在表单 `Form` 的顶部（标题栏下方）创建一个菜单栏，并在组件中放置一个 `MenuStrip` 图标。要选择 `MenuStrip`，请点击此图标。你可以使用设计模式为你的应用程序创建和编辑菜单。菜单项与其他控件一样，具有事件，可以通过属性窗口访问这些事件。

要向菜单中添加项，请点击“在此处输入”文本框。此操作会向菜单中添加 `ToolMenuItem` 条目。按下 Enter 键后，菜单项将添加到菜单中。然后会显示“在此处输入”文本框，允许你在原始菜单项的下方或侧面添加项（15.3）。

要创建快捷键，请在需要下划线的字符前使用和符号 (`&`)。例如，要创建一个字母 F 带下划线的“文件”项，请输入 `&文件`。要显示和符号，请使用 `&&`。要为菜单项添加其他快捷键（例如 Ctrl+F），请设置相应 `ToolMenuItem` 的 `ShortcutKeys` 属性。要执行此操作，请在属性窗口选择该属性右侧的向下箭头。在出现的窗口（15.4）中，使用复选框和下拉列表来选择快捷键。完成后，点击屏幕上的其他地方。你可以通过将 `ShortcutKeys` 属性设置为 `false` 来隐藏快捷键，并通过修改 `ShortcutDisplayString` 来修改快捷键在菜单项中的显示方式。

![](img/57baed2319be0bb1b5f98674846f2711_640_0.png)

在文本框中输入菜单名称 主菜单栏 `MenuStrip` 图标

**图 15.2** 在 Visual Studio 中编辑菜单。

![](img/57baed2319be0bb1b5f98674846f2711_640_1.png)
在菜单中的字母前放置 `&` 字符以带有下划线，以便该字符可以作为访问快捷键。用于添加更多菜单或向所选菜单中添加项的文本框。

**图 15.3** 向 `MenuStrip` 中添加 `ToolMenuItems`。

![](img/57baed2319be0bb1b5f98674846f2711_640_2.png)
选择键（修改菜单的键组合）使用这些复选框来指定修饰键

**图 15.4** 设置菜单项的快捷键。

## 外观观察 15.1

按钮可以具有访问快捷键。在按钮的文本中，所需字符之前立即放置 `&` 符号。要在运行的应用程序中使用其访问快捷键按下按钮，用户需要按下 Alt 键和带下划线的字符。如果程序运行时看不到下划线，请按 Alt 键以显示下划线。

你可以通过选择菜单项并按下 Delete 键来移除菜单项。菜单项可以通过分隔线进行逻辑分组，这可以通过右键点击菜单并选择“插入 > 隔符”来插入。

# 第15章 使用 Windows Forms 构建图形用户界面：第2部分

```sharp
blueToolStripMenuItem.Checked = true;
}

// 更新菜单状态并显示红色颜色
private void redToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // 重置颜色 ToolStripMenuItems 的勾选标记
    ClearColor();
    // 将颜色设置为红色
    displayLabel.ForeColor = Color.Red;
    redToolStripMenuItem.Checked = true;
}

// 更新菜单状态并显示绿色颜色
private void greenToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // 重置颜色 ToolStripMenuItems 的勾选标记
    ClearColor();
    // 将颜色设置为绿色
    displayLabel.ForeColor = Color.Green;
    greenToolStripMenuItem.Checked = false;
}

// 重置字体 ToolStripMenuItems 的勾选标记
private void ClearFont()
{
    // 清除所有勾选标记
    timesToolStripMenuItem.Checked = false;
    courierToolStripMenuItem.Checked = false;
    comicToolStripMenuItem.Checked = false;
}

// 更新菜单状态并将字体设置为 Times New Roman
private void timesToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // 重置字体 ToolStripMenuItems 的勾选标记
    ClearFont();
    // 设置 Times New Roman 字体
    timesToolStripMenuItem.Checked = true;
    displayLabel.Font = new Font("Times New Roman", 14,
    displayLabel.Font.Style);
}
```

**图 15.7** | 使用菜单更改字体颜色和样式。（5 部分中的第 3 部分）

```sharp
112      // 更新菜单状态并将字体设置为 Courier
113      private void courierToolStripMenuItem_Click(
114          object sender, EventArgs e)
115      {
116          // 重置字体 ToolStripMenuItems 的勾选标记
117          ClearFont();
118
119      //设置 Courier 字体
120          courierToolStripMenuItem.Checked = true;
121          displayLabel.Font = new Font("Courier", 14,
122          displayLabel.Font.Style);
123      }
124
125      // 更新菜单状态并将字体设置为 Comic Sans MS
126      private void comicToolStripMenuItem_Click(
127          object sender, EventArgs e)
128      {
129          // 重置字体 ToolStripMenuItems 的勾选标记
130          ClearFont();
131
132      //设置 Comic Sans 字体
133          comicToolStripMenuItem.Checked = true;
134          displayLabel.Font = new Font("Comic Sans MS", 14,
135          displayLabel.Font.Style);
136      }
137
138      // 切换勾选标记并切换粗体样式
139      private void boldToolStripMenuItem_Click(object sender, EventArgs e)
140      {
141          // 切换勾选标记
142          boldToolStripMenuItem.Checked = !boldToolStripMenuItem.Checked;
143      }
144      // 使用 异或切换粗体，保留所有其他样式
145          displayLabel.Font = new Font(displayLabel.Font,
146          displayLabel.Font.Style ^ FontStyle.Bold);
147      }
149
150      // 切换勾选标记并切换斜体样式
151      private void italicToolStripMenuItem_Click(
152          object sender, EventArgs e)
153      {
154          // 切换勾选标记
155          italicToolStripMenuItem.Checked =
156          !italicToolStripMenuItem.Checked;
157      }
158      // 使用 异或切换斜体，保留所有其他样式
159          displayLabel.Font = new Font(displayLabel.Font,
160          displayLabel.Font.Style ^ FontStyle.Italic);
161      }
162  }
```
