
`javax.swing.JRadioButtonMenuItem 1.2`

- `JRadioButtonMenuItem(String label)`  
  使用给定标签构造单选按钮菜单项。
- `JRadioButtonMenuItem(String label, boolean state)`  
  使用给定标签和给定初始状态（true 表示已选中）构造单选按钮菜单项。

`javax.swing.AbstractButton 1.2`

- `boolean isSelected()`
- `void setSelected(boolean state)`  
  获取或设置此项的选择状态（true 表示已选中）。

### 11.5.4 弹出菜单

*弹出菜单*是不依附于菜单栏、而是浮动在某个位置上的菜单（见图 11.18）。

![](img/127bccebb2cfadea3f02579edaad63c3_703_0.png)

**图 11.18** 一个弹出菜单

创建弹出菜单与创建常规菜单一样，只是弹出菜单没有标题。

```
var popup = new JPopupMenu();
```

然后，像往常一样添加菜单项：

```
var item = new JMenuItem("Cut");
item.addActionListener(listener);
popup.add(item);
```

与始终显示在框架顶部的常规菜单栏不同，必须使用 `show` 方法显式显示弹出菜单。指定父组件和弹出菜单的位置，使用父组件的坐标系。例如：

```
popup.show(panel, x, y);
```

通常，你希望在用户单击特定鼠标按钮时弹出菜单——即所谓的*弹出触发器*。在 Windows 和 Linux 中，弹出触发器是非主（通常是右）鼠标按钮。要在用户使用弹出触发器单击组件时弹出菜单，只需调用方法

```
component.setComponentPopupMenu(popup);
```

极少数情况下，你可能将一个组件放在另一个带有弹出菜单的组件内。子组件可以通过调用以下方法继承父组件的弹出菜单：

```
child.setInheritsPopupMenu(true);
```

| `javax.swing.JPopupMenu` | 1.2 |
|---|---|
| `void show(Component c, int x, int y)` | 在组件 c 上方显示弹出菜单，左上角位于 (x, y)（在 c 的坐标空间中）。 |
| `boolean isPopupTrigger(MouseEvent event)` | 1.3 |
|  | 如果鼠标事件是弹出菜单触发器，则返回 true。 |

| `java.awt.event.MouseEvent` | 1.1 |
|---|---|
| `boolean isPopupTrigger()` | 如果此鼠标事件是弹出菜单触发器，则返回 true。 |

### 11.5.5 键盘助记符和加速键

对经验丰富的用户来说，通过*键盘助记符*选择菜单项确实非常方便。可以通过在菜单项构造函数中指定助记字母来为菜单项创建键盘助记符：

```
var aboutItem = new JMenuItem("About", 'A');
```

键盘助记符会自动显示在菜单中，助记字母带下划线（见图 11.19）。例如，在上一个示例定义的菜单项中，标签将显示为“About”，字母 A 带下划线。当菜单显示时，用户只需按 A 键，该菜单项即被选中。（如果助记字母不是菜单字符串的一部分，那么键入它仍会选中该项，但菜单中不会显示该助记符。自然，这种不可见的助记符用处存疑。）

![](img/127bccebb2cfadea3f02579edaad63c3_705_0.png)

**图 11.19** 键盘助记符

有时，你不希望给菜单项中与助记符匹配的第一个字母加下划线。例如，如果菜单项“Save As”的助记符是‘A’，那么给第二个‘A’（Save As）加下划线更有意义。可以通过调用 `setDisplayedMnemonicIndex` 方法指定要加下划线的字符。

如果有一个 Action 对象，可以按如下方式将助记符添加为 `Action.MNEMONIC_KEY` 键的值：

```
aboutAction.putValue(Action.MNEMONIC_KEY, new Integer('A'));
```

只能在菜单项的构造函数中提供助记字母，不能在菜单的构造函数中提供。要为菜单附加助记符，请调用 `setMnemonic` 方法：

```
var helpMenu = new JMenu("Help");
helpMenu.setMnemonic('H');
```

要从菜单栏中选择顶层菜单，请同时按 Alt 键和助记字母。例如，按 Alt+H 从菜单栏中选择 Help 菜单。

键盘助记符让你从当前打开的菜单中选择子菜单或菜单项。相比之下，加速键是键盘快捷键，让你无需打开菜单即可选择菜单项。例如，许多程序将加速键 Ctrl+O 和 Ctrl+S 附加到 File 菜单中的 Open 和 Save 项。使用 `setAccelerator` 方法为菜单项附加加速键。`setAccelerator` 方法接受一个 `KeyStroke` 类型的对象。例如，以下调用将加速键 Ctrl+O 附加到 `openItem` 菜单项：

```
openItem.setAccelerator(KeyStroke.getKeyStroke("ctrl O"));
```

键入加速键组合会自动选择该菜单选项并触发动作事件，就像用户手动选择了该菜单选项一样。

只能将加速键附加到菜单项，不能附加到菜单。加速键实际上不会打开菜单。相反，它们会直接触发与菜单关联的动作事件。

从概念上讲，向菜单项添加加速键类似于向 Swing 组件添加加速键的技术。但是，当加速键添加到菜单项时，该键组合会自动显示在菜单中（见图 11.20）。

![](img/127bccebb2cfadea3f02579edaad63c3_707_0.png)

**图 11.20** 加速键

> **注意：** 在 Windows 下，Alt+F4 会关闭窗口。但这不是要在 Java 中编程的加速键。它是操作系统定义的快捷键。
>
> 无论菜单上是否有 Close 项，此键组合都会为活动窗口触发 `WindowClosing` 事件。

| `javax.swing.JMenuItem` | 1.2 |
|---|---|
| `JMenuItem(String label, int mnemonic)` | 构造一个具有给定标签和助记符的菜单项。 |
| `void setAccelerator(KeyStroke k)` | 将击键 `k` 设置为该菜单项的加速键。加速键显示在标签旁边。 |

| `javax.swing.AbstractButton` | 1.2 |
|---|---|
| `void setMnemonic(int mnemonic)` | 设置按钮的助记字符。该字符将在标签中加下划线。 |
| `void setDisplayedMnemonicIndex(int index)` 1.4 | 设置按钮文本中要加下划线的字符索引。如果你不希望助记字符的第一次出现加下划线，请使用此方法。 |

### 11.5.6 启用和禁用菜单项

有时，某个菜单项只应在特定上下文中被选择。例如，当文档以只读模式打开时，Save 菜单项没有意义。当然，我们可以用 `Menu.remove` 方法从菜单中移除该项，但用户会对内容不断变化的菜单感到惊讶。相反，更好的做法是停用那些会导致暂时不合适命令的菜单项。停用的菜单项显示为灰色，无法选择（见图 11.21）。

![](img/127bccebb2cfadea3f02579edaad63c3_708_0.png)

**图 11.21** 已禁用的菜单项

要启用或禁用菜单项，请使用 `setEnabled` 方法：

```
saveItem.setEnabled(false);
```

启用和禁用菜单项有两种策略。每次情况变化时，你可以对相关菜单项或动作调用 `setEnabled`。例如，一旦文档被设置为只读模式，就可以找到 Save 和 Save As 菜单项并禁用它们。或者，你可以在显示菜单之前禁用这些项。为此，必须为“menu selected”事件注册监听器。`javax.swing.event` 包定义了一个 `MenuListener` 接口，其中包含三个方法：

```
void menuSelected(MenuEvent event)
void menuDeselected(MenuEvent event)
void menuCanceled(MenuEvent event)
```

`menuSelected` 方法在菜单显示*之前*被调用。因此，它可用于禁用或启用菜单项。以下代码展示了每当选中 Read Only 复选框菜单项时，如何禁用 Save 和 Save As 动作：
