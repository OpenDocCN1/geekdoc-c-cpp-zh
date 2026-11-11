

| `javax.swing.ButtonGroup` 1.2 |
|---|
| • `void add(AbstractButton b)`<br>将该按钮添加到组中。<br><br>• `ButtonModel getSelection()`<br>返回所选中按钮的按钮模型。 |

| `javax.swing.ButtonModel` 1.2 |
|---|
| • `String getActionCommand()`<br>返回此按钮模型的动作命令。 |

| `javax.swing.AbstractButton` 1.2 |
|---|
| • `void setActionCommand(String s)`<br>为此按钮及其模型设置动作命令。 |

## 11.4.3 边框

如果窗口中包含多组单选按钮，你可能希望以可视方式指示哪些按钮属于同一组。Swing 为此提供了一组有用的*边框*。你可以将边框应用到任何继承自 `JComponent` 的组件上。最常见的用法是围绕面板放置边框，并用其他用户界面元素（如单选按钮）填充该面板。

你可以从多种边框中进行选择，但所有边框的使用步骤都相同。

1. 调用 `BorderFactory` 的静态方法来创建边框。你可以在以下样式中选择（参见图 11.14）：
   - 凹陷斜面
   - 凸起斜面
   - 蚀刻
   - 直线
   - 哑光
   - 空白（仅用于在组件周围创建一些空白空间）

![](img/127bccebb2cfadea3f02579edaad63c3_685_0.png)

2. 如果需要，可以将边框传递给 `BorderFactory.createTitledBorder` 来为其添加标题。
3. 如果想要更复杂的效果，可以通过调用 `BorderFactory.createCompoundBorder` 将多个边框组合在一起。
4. 调用 `JComponent` 类的 `setBorder` 方法将生成的边框添加到组件上。

例如，下面展示了如何为面板添加带标题的蚀刻边框：

```java
Border etched = BorderFactory.createEtchedBorder();
Border titled = BorderFactory.createTitledBorder(etched, "A Title");
panel.setBorder(titled);
```

不同的边框在设置宽度和颜色时有不同的选项；详情请参阅 API 注释。真正的边框爱好者会注意到，还有一个 `SoftBevelBorder` 类用于创建边角柔化的斜面边框，并且 `LineBorder` 也可以拥有圆角。你只能通过类构造器来构建这些边框——`BorderFactory` 没有对应的方法。

### javax.swing.BorderFactory 1.2

- `static Border createLineBorder(Color color)`
- `static Border createLineBorder(Color color, int thickness)`
  创建简单的直线边框。
- `static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Color color)`
- `static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Icon tileIcon)`
  创建用颜色或重复图标填充的粗边框。
- `static Border createEmptyBorder()`
- `static Border createEmptyBorder(int top, int left, int bottom, int right)`
  创建空白边框。
- `static Border createEtchedBorder()`
- `static Border createEtchedBorder(Color highlight, Color shadow)`
- `static Border createEtchedBorder(int type)`
- `static Border createEtchedBorder(int type, Color highlight, Color shadow)`
  创建具有 3D 效果的边框。`type` 参数是 `EtchedBorder.RAISED`、`EtchedBorder.LOWERED` 之一。
- `static Border createBevelBorder(int type)`
- `static Border createBevelBorder(int type, Color highlight, Color shadow)`
- `static Border createLoweredBevelBorder()`
- `static Border createRaisedBevelBorder()`
  创建具有凹陷或凸起表面效果的边框。`type` 参数是 `BevelBorder.RAISED`、`BevelBorder.LOWERED` 之一。
- `static TitledBorder createTitledBorder(String title)`
- `static TitledBorder createTitledBorder(Border border)`
- `static TitledBorder createTitledBorder(Border border, String title)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position, Font font)`
- `static TitledBorder createTitledBorder(Border border, String title, int justification, int position, Font font, Color color)`
  创建具有指定属性的带标题边框。`justification` 参数是 `TitledBorder` 常量 `LEFT`、`CENTER`、`RIGHT`、`LEADING`、`TRAILING` 或 `DEFAULT_JUSTIFICATION`（左对齐）之一，`position` 是 `ABOVE_TOP`、`TOP`、`BELOW_TOP`、`ABOVE_BOTTOM`、`BOTTOM`、`BELOW_BOTTOM` 或 `DEFAULT_POSITION`（顶部）之一。
- `static CompoundBorder createCompoundBorder(Border outsideBorder, Border insideBorder)`
  将两个边框组合成一个新边框。

### javax.swing.border.SoftBevelBorder 1.2

- `SoftBevelBorder(int type)`
- `SoftBevelBorder(int type, Color highlight, Color shadow)`
  创建边角柔化的斜面边框。`type` 参数是 `SoftBevelBorder.RAISED`、`SoftBevelBorder.LOWERED` 之一。

| `javax.swing.border.LineBorder` 1.2 |
|---|
| • `public LineBorder(Color color, int thickness, boolean roundedCorners)`<br>创建具有指定颜色和粗细的直线边框。如果 `roundedCorners` 为 `true`，则边框具有圆角。 |

| `javax.swing.JComponent` 1.2 |
|---|
| • `void setBorder(Border border)`<br>设置此组件的边框。 |

## 11.4.4 组合框

如果可选选项不止几个，单选按钮并不是一个好的选择，因为它们会占用太多屏幕空间。此时可以改用组合框。当用户点击该组件时，会下拉显示一个选项列表，用户随后可以选择其中一个（参见图 11.15）。

![](img/127bccebb2cfadea3f02579edaad63c3_687_0.png)

**图 11.15** 一个组合框

如果下拉列表框被设置为*可编辑*，你可以像编辑文本字段一样编辑当前选中的内容。因此，这个组件被称为*组合框*——它结合了文本字段的灵活性和一组预定义选项。`JComboBox` 类提供了组合框组件。

自 Java 7 起，`JComboBox` 类是一个泛型类。例如，`JComboBox<String>` 存放 String 类型的对象，而 `JComboBox<Integer>` 存放整数。

调用 `setEditable` 方法可以使组合框可编辑。请注意，编辑操作只会影响当前选中的项目，绝不会改变选项列表本身。

你可以通过调用 `getSelectedItem` 方法获取当前选中的项目——如果组合框是可编辑的，该项目可能已被编辑。但是，对于可编辑的组合框，该项目可能具有任何类型，具体取决于编辑器如何将用户编辑的内容转换为对象（有关编辑器的讨论，请参见卷 II 第 6 章）。如果组合框不可编辑，最好调用

```java
combo.getItemAt(combo.getSelectedIndex())
```

这样会以正确的类型返回选中的项目。

在示例程序中，用户可以从样式列表（Serif、SansSerif、Monospaced 等）中选择字体样式，也可以直接输入其他字体。

使用 `addItem` 方法添加选项。在我们的程序中，只在构造函数中调用了 `addItem`，但你可以随时调用它。

```java
var faceCombo = new JComboBox<String>();
faceCombo.addItem("Serif");
faceCombo.addItem("SansSerif");
. . .
```

此方法会将字符串添加到列表末尾。你可以使用 `insertItemAt` 方法将新项目插入到列表中的任意位置：

```java
faceCombo.insertItemAt("Monospaced", 0); // 添加到开头
```

你可以添加任何类型的项目——组合框会调用每个项目的 `toString` 方法来显示它。

如果需要在运行时移除项目，可以使用 `removeItem` 或 `removeItemAt` 方法，具体取决于你提供的是要移除的项目还是其位置。

```java
faceCombo.removeItem("Monospaced");
faceCombo.removeItemAt(0); // 移除第一个项目
```

`removeAllItems` 方法会一次性移除所有项目。

> **提示：** 如果需要向组合框添加大量项目，`addItem` 方法的性能会较差。此时，可以构造一个 `DefaultComboBoxModel`，通过调用 `addElement` 填充它，然后调用 `JComboBox` 类的 `setModel` 方法。

当用户从组合框中选择一个项目时，组合框会生成一个动作事件。要查看选中了哪个项目，可以在事件参数上调用 `getSource` 来获取发送该事件的组合框引用。

