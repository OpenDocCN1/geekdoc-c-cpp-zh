
```java
public void menuSelected(MenuEvent event)
{
    saveAction.setEnabled(!readonlyItem.isSelected());
    saveAsAction.setEnabled(!readonlyItem.isSelected());
}
```

> ⚠️ **注意：**
>
> 在显示菜单之前禁用菜单项是个聪明的想法，但对于同时带有快捷键的菜单项并不起作用。因为按下快捷键时菜单从未打开，所以该操作从未被禁用，并且仍然会由快捷键触发。

- **javax.swing.JMenuItem 1.2**
  - `void setEnabled(boolean b)` — 启用或禁用该菜单项。

- **javax.swing.event.MenuListener 1.2**
  - `void menuSelected(MenuEvent e)` — 在菜单被选中之后、打开之前调用。
  - `void menuDeselected(MenuEvent e)` — 在菜单取消选中之后、关闭之后调用。
  - `void menuCanceled(MenuEvent e)` — 在菜单被取消时调用，例如用户点击菜单外部时。

清单 11.6 是一个生成一组菜单的示例程序。它展示了你在本节中见过的所有功能：嵌套菜单、禁用的菜单项、复选框和单选按钮菜单项、弹出菜单，以及键盘助记键和快捷键。

### **清单 11.6** menu/MenuFrame.java

```java
 1  package menu;
 2
 3  import java.awt.event.*;
 4  import javax.swing.*;
 5
 6  /**
 7   * A frame with a sample menu bar.
 8   */
 9  public class MenuFrame extends JFrame
10 {
11    private static final int DEFAULT_WIDTH = 300;
12    private static final int DEFAULT_HEIGHT = 200;
13    private Action saveAction;
14    private Action saveAsAction;
15    private JCheckBoxMenuItem readonlyItem;
16    private JPopupMenu popup;
17
18    /**
19     * A sample action that prints the action name to
       System.out.
20     */
21    class TestAction extends AbstractAction
22    {
23      public TestAction(String name)
24      {
25        super(name);
26      }
27
28      public void actionPerformed(ActionEvent event)
29      {
30        System.out.println(getValue(Action.NAME) + "selected.");
31      }
32    }
33
34    public MenuFrame()
35    {
36      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
37
38      var fileMenu = new JMenu("File");
39      fileMenu.add(new TestAction("New"));
40
41      // demonstrate accelerators
42
43      var openItem = fileMenu.add(new TestAction("Open"));
44      openItem.setAccelerator(KeyStroke.getKeyStroke("ctrl O"));
45
46      fileMenu.addSeparator();
47
48      saveAction = new TestAction("Save");
49      JMenuItem saveItem = fileMenu.add(saveAction);
50      saveItem.setAccelerator(KeyStroke.getKeyStroke("ctrl S"));
51
52      saveAsAction = new TestAction("Save As");
53      fileMenu.add(saveAsAction);
54      fileMenu.addSeparator();
55
56      fileMenu.add(new AbstractAction("Exit")
57      {
58        public void actionPerformed(ActionEvent event)
59        {
60          System.exit(0);
61        }
62      });
63
64      // demonstrate checkbox and radio button menus
65
66      readonlyItem = new JCheckBoxMenuItem("Read-only");
102    var optionMenu = new JMenu("Options");
103
104    optionMenu.add(readonlyItem);
105    optionMenu.addSeparator();
106    optionMenu.add(insertItem);
107    optionMenu.add(overtypeItem);
108
109    editMenu.addSeparator();
110    editMenu.add(optionMenu);
111
112    // demonstrate mnemonics
113
114    var helpMenu = new JMenu("Help");
115    helpMenu.setMnemonic('H');
116
117    var indexItem = new JMenuItem("Index");
118    indexItem.setMnemonic('I');
119    helpMenu.add(indexItem);
120
121    // you can also add the mnemonic key to an action
122    var aboutAction = new TestAction("About");
123    aboutAction.putValue(Action.MNEMONIC_KEY,
Integer.valueOf('A'));
124    helpMenu.add(aboutAction);
125
126    // add all top-level menus to menu bar
127
128    var menuBar = new JMenuBar();
129    setJMenuBar(menuBar);
130
131    menuBar.add(fileMenu);
132    menuBar.add(editMenu);
133    menuBar.add(helpMenu);
134
135    // demonstrate pop-ups
136
137    popup = new JPopupMenu();
138    popup.add(cutAction);
139    popup.add(copyAction);
140        popup.add(pasteAction);
141
142        var panel = new JPanel();
143        panel.setComponentPopupMenu(popup);
144        add(panel);
145    }
146 }
```

### 11.5.7 工具栏

工具栏是一个按钮栏，可让用户快速访问程序中最常用的命令（见图 11.22）。

![](img/0e7b74ef51a065c077b42cd87b362288_984_0.png)

**图 11.22** 一个工具栏

工具栏的特别之处在于你可以将其移动到其他位置。你可以将工具栏拖到框架的四个边框之一（见图 11.23）。释放鼠标按钮时，工具栏会停放到新位置（见图 11.24）。

![](img/0e7b74ef51a065c077b42cd87b362288_985_0.png)

**图 11.23** 拖动工具栏

![](img/0e7b74ef51a065c077b42cd87b362288_985_1.png)

**图 11.24** 工具栏已被拖动到另一个边框

**注意：**

如果工具栏位于使用边框布局或任何其他支持北、东、南、西约束的布局管理器的容器中，则工具栏拖动功能可用。

工具栏甚至可以完全从框架中分离出来。分离的工具栏包含在它自己的框架中（见图 11.25）。当你关闭包含分离工具栏的框架时，工具栏会跳回原来的框架。

![](img/0e7b74ef51a065c077b42cd87b362288_986_0.png)

**图 11.25** 分离工具栏

工具栏的编程很直接。将组件添加到工具栏中：

```java
var toolbar = new JToolBar();
toolbar.add(blueButton);
```

JToolBar 类还有一个添加 Action 对象的方法。只需像下面这样用 Action 对象填充工具栏：

```java
toolbar.add(blueAction);
```

操作的小图标会显示在工具栏中。

你可以用分隔符分隔按钮组：

```java
toolbar.addSeparator();
```

例如，图 11.22 中的工具栏在第三个和第四个按钮之间有一个分隔符。

然后，将工具栏添加到框架中：

```java
add(toolbar, BorderLayout.NORTH);
```

你还可以为工具栏指定一个标题，该标题会在工具栏取消停靠时显示：

```java
toolbar = new JToolBar(titleString);
```

默认情况下，工具栏最初是水平的。要让工具栏一开始就是垂直的，请使用

```java
toolbar = new JToolBar(SwingConstants.VERTICAL);
```

或

```java
toolbar = new JToolBar(titleString, SwingConstants.VERTICAL);
```

按钮是工具栏中最常见的组件。但你可以添加到工具栏中的组件没有限制。例如，你可以向工具栏添加一个组合框。

### 11.5.8 工具提示

工具栏的一个缺点是用户常常对工具栏中微小图标的含义感到困惑。为了解决这个问题，用户界面设计者发明了*工具提示*。当光标在按钮上停留片刻时，工具提示会被激活。工具提示文本显示在一个彩色矩形内。当用户将鼠标移开时，工具提示消失。（见[图 11.26](#)。）

![](img/0e7b74ef51a065c077b42cd87b362288_988_0.png)

**图 11.26** 一个工具提示

在 Swing 中，只需调用 setToolTipText 方法，就可以向任何 JComponent 添加工具提示：

```java
exitButton.setToolTipText("Exit");
```

或者，如果你使用 Action 对象，可以将工具提示与 SHORT_DESCRIPTION 键关联：

```java
exitAction.putValue(Action.SHORT_DESCRIPTION, "Exit");
```

### javax.swing.JToolBar 1.2

- `JToolBar()`
- `JToolBar(String titleString)`
- `JToolBar(int orientation)`
- `JToolBar(String titleString, int orientation)`

构造一个具有给定标题字符串和方向的工具栏。orientation 是 SwingConstants.HORIZONTAL（默认值）或 SwingConstants.VERTICAL 之一。

- `JButton add(Action a)` — 在工具栏内构造一个新按钮，其名称、图标、简短描述和操作回调来自给定的 action，并将该按钮添加到工具栏末尾。
- `void addSeparator()` — 在工具栏末尾添加一个分隔符。

### javax.swing.JComponent 1.2

- `void setToolTipText(String text)` — 设置当鼠标悬停在该组件上时应显示为工具提示的文本。

## 11.6 复杂的布局管理

到目前为止，我们在示例应用程序的用户界面中只使用了边框布局、流式布局和网格布局。对于更复杂的任务，这还不够。

自 Java 1.0 起，AWT 就包含了*网格包布局*，它按行和列布置组件。行和列的大小可以灵活调整，组件可以跨越多行和多列。这个布局管理器非常灵活，但也非常复杂。众所周知，仅仅提到“网格包布局”这个词，就会让 Java 程序员心生畏惧。

Swing 设计者曾试图设计一种布局管理器，以将程序员从网格包布局的暴政中解放出来，但这一尝试并未成功，他们由此提出了*箱式布局*。根据 `BoxLayout` 类的 JDK 文档：“将多个面板以不同的水平和垂直[原文如此]组合进行嵌套，会产生类似于 `GridBagLayout` 的效果，而没有那么复杂。”然而，由于每个箱都是独立布局的，你不能使用箱式布局来同时水平和垂直地排列相邻组件。
