

- `JSlider(int direction, int min, int max, int initialValue)`  
  使用给定的方向以及最小值、最大值和初始值构造一个水平滑块。direction 参数取 `SwingConstants.HORIZONTAL` 或 `SwingConstants.VERTICAL` 之一，默认为水平。最小值、初始值和最大值的默认值分别为 0、50 和 100。
- `void setPaintTicks(boolean b)`  
  如果 b 为 true，则显示刻度。
- `void setMajorTickSpacing(int units)`
- `void setMinorTickSpacing(int units)`  
  按给定滑块单位的倍数设置主刻度或次刻度。
- `void setPaintLabels(boolean b)`  
  如果 b 为 true，则显示刻度标签。
- `void setLabelTable(Dictionary table)`  
  设置用于刻度标签的组件。表中的每个键/值对采用 `Integer.valueOf(value)/component` 的形式。
- `void setSnapToTicks(boolean b)`  
  如果 b 为 true，则滑块在每次调整后自动吸附到最近的刻度。
- `void setPaintTrack(boolean b)`  
  如果 b 为 true，则显示滑块运行的轨道。

## 11.5 菜单

本章开始时介绍了你可能希望放入窗口的最常见组件，例如各种按钮、文本框和组合框。Swing 还支持另一种用户界面元素——下拉菜单，这在 GUI 应用程序中很常见。

窗口顶部的*菜单栏*包含下拉菜单的名称。单击名称会打开包含*菜单项*和子菜单的*菜单*。当用户单击某个菜单项时，所有菜单都会关闭，并向程序发送一条消息。图 11.17 显示了一个带有子菜单的典型菜单。

![](img/0e7b74ef51a065c077b42cd87b362288_964_0.png)

**图 11.17** 带子菜单的菜单

### 11.5.1 菜单构建

构建菜单非常简单。首先，创建一个菜单栏：

```java
var menuBar = new JMenuBar();
```

菜单栏只是一个可以放在任何位置的组件。通常，你希望它出现在框架顶部。可以使用 `setJMenuBar` 方法将其添加到那里：

```java
frame.setJMenuBar(menuBar);
```

每个菜单创建一个菜单对象：

```java
var editMenu = new JMenu("Edit");
```

将顶级菜单添加到菜单栏：

```java
menuBar.add(editMenu);
```

将菜单项、分隔符和子菜单添加到菜单对象：

```java
var pasteItem = new JMenuItem("Paste");
editMenu.add(pasteItem);
editMenu.addSeparator();
JMenu optionsMenu = . . .; // 一个子菜单
editMenu.add(optionsMenu);
```

在 [图 11.17](#) 中，你可以看到“Paste”和“Read-only”菜单项下方的分隔符。

当用户选择某个菜单项时，会触发一个动作事件。你需要为每个菜单项安装一个动作监听器：

```java
ActionListener listener = . . .;
pasteItem.addActionListener(listener);
```

方法 `JMenu.add(String s)` 可以方便地将菜单项添加到菜单末尾。例如：

```java
editMenu.add("Paste");
```

`add` 方法返回创建的菜单项，因此你可以捕获它并添加监听器，如下所示：

```java
JMenuItem pasteItem = editMenu.add("Paste");
pasteItem.addActionListener(listener);
```

菜单项经常触发也可以通过其他用户界面元素（如工具栏按钮）激活的命令。在 第 623 页的 [10.4.5 节“动作”](#) 中，你看到了如何通过 `Action` 对象指定命令。你可以定义一个实现 `Action` 接口的类，通常通过扩展 `AbstractAction` 便捷类来实现；在 `AbstractAction` 对象的构造函数中指定菜单项标签，并重写 `actionPerformed` 方法来放置菜单动作处理程序。例如：

```java
var exitAction = new AbstractAction("Exit") // 菜单项文本放在这里
{
    public void actionPerformed(ActionEvent event)
    {
        // 动作代码放在这里
        System.exit(0);
    }
};
```

然后可以将动作添加到菜单中：

```java
JMenuItem exitItem = fileMenu.add(exitAction);
```

此命令使用动作名称将一个菜单项添加到菜单中，动作对象成为其监听器。这只是以下代码的便捷简写：

```java
var exitItem = new JMenuItem(exitAction);
fileMenu.add(exitItem);
```

#### `javax.swing.JMenu` 1.2

- `JMenu(String label)`  
  使用给定标签构造一个菜单。
- `JMenuItem add(JMenuItem item)`  
  添加一个菜单项（或一个菜单）。
- `JMenuItem add(String label)`  
  将具有给定标签的菜单项添加到此菜单并返回该项。
- `JMenuItem add(Action a)`  
  将具有给定动作的菜单项添加到此菜单并返回该项。
- `void addSeparator()`  
  向菜单添加一条分隔线。
- `JMenuItem insert(JMenuItem menu, int index)`  
  在指定索引处向菜单添加新的菜单项（或子菜单）。
- `JMenuItem insert(Action a, int index)`  
  在指定索引处添加具有给定动作的新菜单项。
- `void insertSeparator(int index)`  
  向菜单添加分隔符。
- `void remove(int index)`
- `void remove(JMenuItem item)`  
  从菜单中移除特定项。

#### `javax.swing.JMenuItem` 1.2

- `JMenuItem(String label)`  
  使用给定标签构造一个菜单项。
- `JMenuItem(Action a)` 1.3  
  为给定动作构造一个菜单项。

#### `javax.swing.AbstractButton` 1.2

- `void setAction(Action a)` 1.3  
  为此按钮或菜单项设置动作。

#### `javax.swing.JFrame` 1.2

- `void setJMenuBar(JMenuBar menubar)`  
  为此框架设置菜单栏。

### 11.5.2 菜单项中的图标

菜单项与按钮非常相似。实际上，`JMenuItem` 类扩展了 `AbstractButton` 类。与按钮一样，菜单可以只有文本标签、只有图标，或者两者都有。你可以使用 `JMenuItem(String, Icon)` 或 `JMenuItem(Icon)` 构造函数来指定图标，也可以使用 `JMenuItem` 类从 `AbstractButton` 类继承的 `setIcon` 方法来设置图标。下面是一个示例：

```java
var cutItem = new JMenuItem("Cut", new ImageIcon("cut.gif"));
```

在图 11.17 中，你可以看到多个菜单项旁边有图标。默认情况下，菜单项文本位于图标的右侧。如果你希望文本位于左侧，请调用 `JMenuItem` 类从 `AbstractButton` 类继承的 `setHorizontalTextPosition` 方法。例如，调用

```java
cutItem.setHorizontalTextPosition(SwingConstants.LEFT);
```

会将菜单项文本移动到图标左侧。

你也可以向动作添加图标：

```java
cutAction.putValue(Action.SMALL_ICON, new ImageIcon("cut.gif"));
```

每当你从一个 `Action` 构造菜单项时，`Action.NAME` 的值会成为菜单项的文本，`Action.SMALL_ICON` 的值会成为图标。

或者，你也可以在 `AbstractAction` 构造函数中设置图标：

```java
cutAction = new AbstractAction("Cut", new ImageIcon("cut.gif"))
{
    public void actionPerformed(ActionEvent event)
    {
        . . .
    }
};
```

#### `javax.swing.JMenuItem` 1.2

- `JMenuItem(String label, Icon icon)`  
  使用给定标签和图标构造一个菜单项。

#### `javax.swing.AbstractButton` 1.2

- `void setHorizontalTextPosition(int pos)`  
  设置文本相对于图标的水平位置。`pos` 参数为 `SwingConstants.RIGHT`（文本在图标右侧）或 `SwingConstants.LEFT`（文本在图标左侧）。

#### `javax.swing.AbstractAction` 1.2

- `AbstractAction(String name, Icon smallIcon)`  
  使用给定名称和图标构造一个抽象动作。

### 11.5.3 复选框和单选按钮菜单项

*复选框*和*单选按钮菜单项*会在名称旁边显示一个复选框或单选按钮（参见 [图 11.17](#)）。当用户选择该菜单项时，该项会自动在选中和未选中状态之间切换。

除了按钮装饰之外，请像对待任何其他菜单项一样对待这些菜单项。例如，下面是如何创建复选框菜单项：

```java
var readonlyItem = new JCheckBoxMenuItem("Read-only");
optionsMenu.add(readonlyItem);
```

单选按钮菜单项的工作方式与普通单选按钮类似。你必须将它们添加到按钮组中。当组中的一个按钮被选中时，其他所有按钮都会自动取消选中。

```java
var group = new ButtonGroup();
var insertItem = new JRadioButtonMenuItem("Insert");
insertItem.setSelected(true);
var overtypeItem = new JRadioButtonMenuItem("Overtype");
group.add(insertItem);
group.add(overtypeItem);
optionsMenu.add(insertItem);
optionsMenu.add(overtypeItem);
```

对于这些菜单项，你不一定需要在用户选择该项时收到通知。相反，你可以直接使用 `isSelected` 方法来测试菜单项的当前状态。（当然，这意味着你应该将菜单项的引用保存在实例字段中。）使用 `setSelected` 方法设置状态。

| 类 | 版本 |
| --- | --- |
| `javax.swing.JCheckBoxMenuItem` | 1.2 |

