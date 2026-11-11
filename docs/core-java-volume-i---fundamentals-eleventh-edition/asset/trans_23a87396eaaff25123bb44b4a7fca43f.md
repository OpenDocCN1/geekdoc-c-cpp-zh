
```java
    public void menuSelected(MenuEvent event)
    {
        saveAction.setEnabled(!readonlyItem.isSelected());
        saveAsAction.setEnabled(!readonlyItem.isSelected());
    }
```

> **注意：** 在显示菜单之前禁用菜单项是个巧妙的想法，但对于同时具有加速键的菜单项并不起作用。因为按下加速键时菜单从未打开，所以该操作从未被禁用，并且仍会由加速键触发。

| javax.swing.JMenuItem 1.2 |
|---|
| • `void setEnabled(boolean b)`<br>启用或禁用该菜单项。 |

| javax.swing.event.MenuListener 1.2 |
|---|
| • `void menuSelected(MenuEvent e)`<br>在菜单已被选中、尚未打开时调用。 |
| • `void menuDeselected(MenuEvent e)`<br>在菜单已被取消选中、关闭之后调用。 |
| • `void menuCanceled(MenuEvent e)`<br>在菜单已被取消时调用，例如用户点击菜单外部。 |

程序清单 11.6 是一个生成一组菜单的示例程序。它展示了你在本节中看到的所有特性：嵌套菜单、禁用的菜单项、复选框和单选按钮菜单项、弹出菜单，以及键盘助记符和加速键。

**程序清单 11.6** menu/MenuFrame.java

```java
    1 package menu;
    2
    3 import java.awt.event.*;
    4 import javax.swing.*;
    5
/**
 * A frame with a sample menu bar.
 */
public class MenuFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;
   private Action saveAction;
   private Action saveAsAction;
   private JCheckBoxMenuItem readonlyItem;
   private JPopupMenu popup;

   /**
    * A sample action that prints the action name to System.out.
    */
   class TestAction extends AbstractAction
   {
      public TestAction(String name)
      {
         super(name);
      }

      public void actionPerformed(ActionEvent event)
      {
         System.out.println(getValue(Action.NAME) + " selected.");
      }
   }

   public MenuFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      var fileMenu = new JMenu("File");
      fileMenu.add(new TestAction("New"));

      // demonstrate accelerators

      var openItem = fileMenu.add(new TestAction("Open"));
      openItem.setAccelerator(KeyStroke.getKeyStroke("ctrl O"));

      fileMenu.addSeparator();

      saveAction = new TestAction("Save");
      JMenuItem saveItem = fileMenu.add(saveAction);
      saveItem.setAccelerator(KeyStroke.getKeyStroke("ctrl S"));

      saveAsAction = new TestAction("Save As");
fileMenu.add(saveAsAction);
fileMenu.addSeparator();

fileMenu.add(new AbstractAction("Exit")
{
   public void actionPerformed(ActionEvent event)
   {
      System.exit(0);
   }
});

// demonstrate checkbox and radio button menus

readonlyItem = new JCheckBoxMenuItem("Read-only");
readonlyItem.addActionListener(new ActionListener()
{
   public void actionPerformed(ActionEvent event)
   {
      boolean saveOk = !readonlyItem.isSelected();
      saveAction.setEnabled(saveOk);
      saveAsAction.setEnabled(saveOk);
   }
});

var group = new ButtonGroup();

var insertItem = new JRadioButtonMenuItem("Insert");
insertItem.setSelected(true);
var overtypeItem = new JRadioButtonMenuItem("Overtype");

group.add(insertItem);
group.add(overtypeItem);

// demonstrate icons

var cutAction = new TestAction("Cut");
cutAction.putValue(Action.SMALL_ICON, new ImageIcon("cut.gif"));
var copyAction = new TestAction("Copy");
copyAction.putValue(Action.SMALL_ICON, new ImageIcon("copy.gif"));
var pasteAction = new TestAction("Paste");
pasteAction.putValue(Action.SMALL_ICON, new ImageIcon("paste.gif"));

var editMenu = new JMenu("Edit");
editMenu.add(cutAction);
editMenu.add(copyAction);
editMenu.add(pasteAction);

// demonstrate nested menus
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
123    aboutAction.putValue(Action.MNEMONIC_KEY, new Integer('A'));
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
140    popup.add(pasteAction);
141
142    var panel = new JPanel();
143    panel.setComponentPopupMenu(popup);
144    add(panel);
145    }
146    }
```

### 11.5.7 工具栏

工具栏是一个按钮栏，可让用户快速访问程序中最常用的命令（见图11.22）。

![](img/127bccebb2cfadea3f02579edaad63c3_713_0.png)

图11.22 工具栏

工具栏的特别之处在于你可以将它们移到别处。你可以将工具栏拖到框架的四个边框之一（见图11.23）。松开鼠标按钮时，工具栏会停放到新位置（见图11.24）。

![](img/127bccebb2cfadea3f02579edaad63c3_713_1.png)

图11.23 拖动工具栏

> 注意：如果工具栏位于使用边框布局或其他支持北、东、南、西约束的布局管理器的容器内，则工具栏拖动功能有效。

![](img/127bccebb2cfadea3f02579edaad63c3_716_0.png)

**图11.26** 工具提示

| javax.swing.JToolBar | 1.2 |
|---|---|
| • `JToolBar()` | |
| • `JToolBar(String titleString)` | |
| • `JToolBar(int orientation)` | |
| • `JToolBar(String titleString, int orientation)` | 用给定的标题字符串和方向构造一个工具栏。orientation 是 `SwingConstants.HORIZONTAL`（默认值）或 `SwingConstants.VERTICAL` 之一。 |
| • `JButton add(Action a)` | 根据给定动作中的名称、图标、简短描述和动作回调，在工具栏内构造一个新按钮，并将该按钮添加到工具栏末尾。 |
| • `void addSeparator()` | 在工具栏末尾添加一个分隔符。 |

| javax.swing.JComponent | 1.2 |
|---|---|
| • `void setToolTipText(String text)` | 设置当鼠标悬停在该组件上时应作为工具提示显示的文本。 |

## 11.6 复杂的布局管理

到目前为止，我们的示例应用程序的用户界面只使用了边框布局、流布局和网格布局。对于更复杂的任务，这还不够。

自 Java 1.0 起，AWT 就包含了*网格包布局（grid bag layout）*，它按行和列布置组件。行和列的大小是灵活的，组件可以跨多行和多列。这个布局管理器非常灵活，但也非常复杂。仅仅提到“网格包布局”这几个字，就足以让 Java 程序员心生畏惧。

为了设计一种能让程序员摆脱网格包布局束缚的布局管理器，Swing 设计者进行了一次不成功的尝试，提出了*箱式布局（box layout）*。根据 BoxLayout 类的 JDK 文档：“使用不同的水平和垂直组合嵌套多个面板，可以得到类似于 GridBagLayout 的效果，而没有其复杂性。”然而，由于每个箱体都是独立布局的，你无法使用箱式布局来同时水平和垂直地排列相邻组件。

Java 1.4 又进行了一次设计网格包布局替代方案的尝试——*弹簧布局（spring layout）*，其中你使用想象中的“弹簧”来连接容器中的组件。当容器调整大小时，弹簧会拉伸或收缩，从而调整组件的位置。这听起来既繁琐又令人困惑，而事实也确实如此。弹簧布局很快便湮没无闻。

NetBeans IDE 结合了一个布局工具（称为“Matisse”）和一个布局管理器。用户界面设计者使用该工具将组件拖放到容器中，并指明哪些组件应当对齐。该工具会将设计者的意图转换为*组布局管理器（group layout manager）*的指令。这比手工编写布局管理代码要方便得多。

在接下来的几节中，我们将介绍网格包布局，因为它很常用，而且仍然是通 过程序化方式生成布局代码的最简单机制。我们将向你展示一种策略，使网格包布局在常见情况下相对轻松。

最后，你将看到如何编写自己的布局管理器。

### 11.6.1 网格包布局

网格包布局是所有布局管理器之母。你可以把网格包布局看作没有限制的网格布局。在网格包布局中，行和列可以具有可变大小。你可以合并相邻单元格，为更大的组件腾出空间。（许多文字处理器以及 HTML 都为表格提供了类似能力：你可以先从一个网格开始，然后根据需要合并相邻单元格。）组件不必填满整个单元格区域，你还可以指定它们在单元格内的对齐方式。

考虑图11.27中的字体选择器。它由以下组件组成：
