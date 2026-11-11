
## 清单 11.5 *（续）*

```java
101 slider.setPaintLabels(true);
102 slider.setSnapToTicks(true);
103 slider.setMajorTickSpacing(20);
104 slider.setMinorTickSpacing(20);

106 labelTable = new Hashtable<Integer, Component>();

108 // add card images

110 labelTable.put(0, new JLabel(new ImageIcon("nine.gif")));
111 labelTable.put(20, new JLabel(new ImageIcon("ten.gif")));
112 labelTable.put(40, new JLabel(new ImageIcon("jack.gif")));
113 labelTable.put(60, new JLabel(new ImageIcon("queen.gif")));
114 labelTable.put(80, new JLabel(new ImageIcon("king.gif")));
115 labelTable.put(100, new JLabel(new ImageIcon("ace.gif")));

117 slider.setLabelTable(labelTable);
118 addSlider(slider, "Icon labels");

120 // add the text field that displays the slider value

122 textField = new JTextField();
123 add(sliderPanel, BorderLayout.CENTER);
124 add(textField, BorderLayout.SOUTH);
125 pack();
126 }

128 /**
129  * Adds a slider to the slider panel and hooks up the listener
130  * @param slider the slider
131  * @param description the slider description
132  */
133 public void addSlider(JSlider slider, String description)
134 {
135    slider.addChangeListener(listener);
136    var panel = new JPanel();
137    panel.add(slider);
138    panel.add(new JLabel(description));
139    panel.setAlignmentX(Component.LEFT_ALIGNMENT);
140    var gbc = new GridBagConstraints();
141    gbc.gridy = sliderPanel.getComponentCount();
142    gbc.anchor = GridBagConstraints.WEST;
143    sliderPanel.add(panel, gbc);
144 }
145 }
```

**javax.swing.JSlider** 1.2

- `JSlider()`
- `JSlider(int direction)`
- `JSlider(int min, int max)`
- `JSlider(int min, int max, int initialValue)`
- `JSlider(int direction, int min, int max, int initialValue)`

  构造一个具有给定方向以及最小值、最大值和初始值的水平滑块。direction 参数为 `SwingConstants.HORIZONTAL` 或 `SwingConstants.VERTICAL` 之一。默认为水平。最小值、初始值和最大值的默认值分别为 0、50 和 100。

- `void setPaintTicks(boolean b)`  
  如果 b 为 true，则显示刻度。

- `void setMajorTickSpacing(int units)`
- `void setMinorTickSpacing(int units)`  
  以给定滑块单位的倍数设置主刻度或次刻度。

- `void setPaintLabels(boolean b)`  
  如果 b 为 true，则显示刻度标签。

- `void setLabelTable(Dictionary table)`  
  设置用于刻度标签的组件。表中的每个键/值对的形式为 `new Integer(value)/component`。

- `void setSnapToTicks(boolean b)`  
  如果 b 为 true，则滑块在每次调整后吸附到最近的刻度。

- `void setPaintTrack(boolean b)`  
  如果 b 为 true，则显示滑块在其上运行的轨道。

## 11.5 菜单

本章开始时，我们介绍了你可能想要放入窗口的最常见组件，例如各种按钮、文本字段和组合框。Swing 还支持另一种用户界面元素——GUI 应用程序中常见的下拉菜单。

窗口顶部的菜单栏包含下拉菜单的名称。单击某个名称会打开包含菜单项和子菜单的菜单。当用户单击菜单项时，所有菜单都会关闭，并向程序发送一条消息。图 11.17 展示了一个带子菜单的典型菜单。

`JMenu.add(String s)` 方法可以方便地将菜单项添加到菜单末尾。例如：

```java
editMenu.add("Paste");
```

add 方法返回创建的菜单项，因此你可以捕获它并添加监听器，如下所示：

```java
JMenuItem pasteItem = editMenu.add("Paste");
pasteItem.addActionListener(listener);
```

菜单项触发的命令也常常可以通过其他用户界面元素（例如工具栏按钮）激活。在第 10.4.5 节“动作”（第 608 页）中，你看到了如何通过 Action 对象指定命令。你定义一个实现 Action 接口的类，通常通过扩展 AbstractAction 便利类来实现，在 AbstractAction 对象的构造函数中指定菜单项标签，并覆盖 actionPerformed 方法以容纳菜单动作处理器。例如：

```java
var exitAction = new AbstractAction("Exit") // menu item text goes here
{
    public void actionPerformed(ActionEvent event)
    {
        // action code goes here
        System.exit(0);
    }
};
```

然后可以将该动作添加到菜单：

```java
JMenuItem exitItem = fileMenu.add(exitAction);
```

此命令使用动作名称将菜单项添加到菜单。动作对象成为其监听器。这只是以下代码的便捷快捷方式：

```java
var exitItem = new JMenuItem(exitAction);
fileMenu.add(exitItem);
```

| `javax.swing.JMenu` 1.2 |
|---|
| • `JMenu(String label)` 构造一个具有给定标签的菜单。<br>• `JMenuItem add(JMenuItem item)` 添加一个菜单项（或一个菜单）。 |

| `javax.swing.JMenu` 1.2 *（续）* |
|---|
| • `JMenuItem add(String label)`<br>将具有给定标签的菜单项添加到此菜单并返回该项。<br><br>• `JMenuItem add(Action a)`<br>将具有给定动作的菜单项添加到此菜单并返回该项。<br><br>• `void addSeparator()`<br>向菜单添加分隔线。<br><br>• `JMenuItem insert(JMenuItem menu, int index)`<br>在特定索引处向菜单添加新菜单项（或子菜单）。<br><br>• `JMenuItem insert(Action a, int index)`<br>在特定索引处添加具有给定动作的新菜单项。<br><br>• `void insertSeparator(int index)`<br>向菜单添加分隔符。<br><br>• `void remove(int index)`<br>• `void remove(JMenuItem item)`<br>从菜单中移除特定项。 |

| `javax.swing.JMenuItem` 1.2 |
|---|
| • `JMenuItem(String label)`<br>构造一个具有给定标签的菜单项。<br><br>• `JMenuItem(Action a)` 1.3<br>为给定动作构造一个菜单项。 |

| `javax.swing.AbstractButton` 1.2 |
|---|
| • `void setAction(Action a)` 1.3<br>设置此按钮或菜单项的动作。 |

| `javax.swing.JFrame` 1.2 |
|---|
| • `void setJMenuBar(JMenuBar menubar)`<br>设置此框架的菜单栏。 |

## 第3部分 基础数据类型

Python中的基本数据类型包括整型（int）、浮点型（float）、字符串（str）、布尔型（bool）和空值（None）。这些类型是构建所有程序的基础。

### 3.1 数值类型

**整型（int）**：任意大小的整数，支持四则运算。例如：`a = 10`，`b = -3`。

**浮点型（float）**：带小数的数字，使用IEEE 754标准存储。例如：`pi = 3.14159`。

**布尔型（bool）**：只有`True`和`False`两个值，常用于条件判断。

```python
# 数值类型示例
x = 42          # 整型
y = 3.14        # 浮点型
z = True        # 布尔型
print(type(x))  # <class 'int'>
```

> **提示**：Python 3中整型没有大小限制，但浮点型会有精度损失，请谨慎比较浮点数。

### 3.2 字符串类型

字符串是由单引号、双引号或三引号括起来的字符序列。支持索引、切片和拼接操作。

| 操作 | 示例 | 结果 |
|------|------|------|
| 索引 | `s[0]` | `'P'` |
| 切片 | `s[1:5]` | `'ython'` |
| 拼接 | `'Py' + 'thon'` | `'Python'` |
| 重复 | `'A' * 3` | `'AAA'` |

三引号字符串支持多行文本，常用于文档字符串和注释。

| `javax.swing.AbstractAction` | `1.2` |
|---|---|
| • `AbstractAction(String name, Icon smallIcon)` | 构造一个具有给定名称和图标的抽象动作。 |

### 11.5.3 复选框和单选按钮菜单项

*复选框*和*单选按钮*菜单项会在名称旁边显示复选框或单选按钮（见图 11.17）。当用户选择该菜单项时，该项会自动在选中和未选中之间切换。

除了按钮装饰之外，像对待任何其他菜单项一样对待这些菜单项。例如，下面是如何创建复选框菜单项：

```java
var readonlyItem = new JCheckBoxMenuItem("Read-only");
optionsMenu.add(readonlyItem);
```

单选按钮菜单项的工作方式与常规单选按钮一样。你必须将它们添加到按钮组中。当组中的一个按钮被选中时，所有其他按钮会自动取消选中。

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

对于这些菜单项，你不一定希望在用户选择菜单项时收到通知。相反，你可以直接使用 `isSelected` 方法测试菜单项的当前状态。（当然，这意味着你应该将菜单项的引用保存在实例字段中。）使用 `setSelected` 方法设置状态。

| `javax.swing.JCheckBoxMenuItem` | `1.2` |
|---|---|
| • `JCheckBoxMenuItem(String label)` | 构造具有给定标签的复选框菜单项。 |
| • `JCheckBoxMenuItem(String label, boolean state)` | 构造具有给定标签和给定初始状态的复选框菜单项（true 表示选中）。 |

