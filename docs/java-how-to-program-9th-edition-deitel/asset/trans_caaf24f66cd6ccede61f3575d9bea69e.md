

JButton button3 接下来被添加（第 57–59 行）。weightx 值和 weighty 值都设置为零，fill 的值为 BOTH。JButton button3 在窗口被调整大小时会增长——它受 button2 的权重值影响。button2 的 weightx 值远大于 button3 的 weightx 值。调整大小时，button2 将占据新空间的更大比例。该按钮放置在第 1 行、第 2 列。占用一行一列。

JTextField textField（第 62 行）和 JTextArea textArea2（第 65 行）的 weightx 值为 0，weighty 值为 0。fill 的值为 BOTH。JTextField 放置在第 3 行、第 0 列，JTextArea 放置在第 3 行、第 2 列。JTextField 占用一行两列，JTextArea 占用一行一列。

方法 addComponent 的参数为 Component 引用 component 以及整数 row、column、width 和 height。第 72–73 行设置 GridBagConstraints 变量 gridx 和 gridy。gridx 变量被赋值为 Component 将被放置的列，gridy 值被赋值为 Component 将被放置的行。第 74–75 行设置 GridBagConstraints 变量 gridwidth 和 gridheight。gridwidth 变量指定 Component 在网格中将跨越的列数，gridheight 变量指定 Component 在网格中将跨越的行数。第 76 行为 GridBagLayout 中的组件设置 GridBagConstraints。GridBagLayout 类的 setConstraints 方法接受一个 Component 参数和一个 GridBagConstraints 参数。第 77 行将组件添加到 JFrame。

执行此应用程序时，尝试调整窗口大小以查看每个 GUI 组件的约束如何影响其在窗口中的位置和大小。

## GridBagConstraints 常量 RELATIVE 和 REMAINDER

代替 gridx 和 gridy，GridBagLayout 的一种变体使用 GridBagConstraints 常量 RELATIVE 和 REMAINDER。RELATIVE 指定某一行中倒数第二个组件应放置在该行中前一个组件的右侧。REMAINDER 指定组件是该行中的最后一个组件。任何不是该行倒数第二个或最后一个组件的组件都必须为 GridBagConstraints 变量 gridwidth 和 gridheight 指定值。图 25.23–25.24 中的应用程序使用这些常量在 GridBagLayout 中排列组件。

```
// Fig. 25.23: GridBagFrame2.java
// Demonstrating GridBagLayout constants.
import java.awt.GridBagLayout;
import java.awt.GridBagConstraints;
import java.awt.Component;
import javax.swing.JFrame;
import javax.swing.JComboBox;
import javax.swing.JTextField;
import javax.swing.JList;
import javax.swing.JButton;

public class GridBagFrame2 extends JFrame
{
    private GridBagLayout layout; // layout of this frame
    private GridBagConstraints constraints; // constraints of this layout
```

Fig. 25.23 | GridBagConstraints constants RELATIVE and REMAINDER. (Part 1 of 3.)

```
16
17 // set up GUI
18 public GridBagFrame2()
19 {
20     super( "GridBagLayout" );
21     layout = new GridBagLayout();
22     setLayout( layout ); // set frame layout
23     constraints = new GridBagConstraints(); // instantiate constraints
24
25     // create GUI components
26     String[] metals = { "Copper", "Aluminum", "Silver" };
27     JComboBox comboBox = new JComboBox( metals );
28
29     JTextField textField = new JTextField( "TextField" );
30
31     String[] fonts = { "Serif", "Monospaced" };
32     JList list = new JList( fonts );
33
34     String[] names = { "zero", "one", "two", "three", "four" };
35     JButton[] buttons = new JButton[ names.length ];
36
37     for ( int count = 0; count < buttons.length; count++ )
38         buttons[ count ] = new JButton( names[ count ] );
39
40     // define GUI component constraints for textField
41     constraints.weightx = 1;
42     constraints.weighty = 1;
43     constraints.fill = GridBagConstraints.BOTH;
44     constraints.gridwidth = GridBagConstraints.REMAINDER;
45     addComponent( textField );
46
47     // buttons[0] -- weightx and weighty are 1: fill is BOTH
48     constraints.gridwidth = 1;
49     addComponent( buttons[ 0 ] );
50
51     // buttons[1] -- weightx and weighty are 1: fill is BOTH
52     constraints.gridwidth = GridBagConstraints.RELATIVE;
53     addComponent( buttons[ 1 ] );
54
55     // buttons[2] -- weightx and weighty are 1: fill is BOTH
56     constraints.gridwidth = GridBagConstraints.REMAINDER;
57     addComponent( buttons[ 2 ] );
58
59     // comboBox -- weightx is 1: fill is BOTH
60     constraints.weighty = 0;
61     constraints.gridwidth = GridBagConstraints.REMAINDER;
62     addComponent( comboBox );
63
64     // buttons[3] -- weightx is 1: fill is BOTH
65     constraints.weighty = 1;
66     constraints.gridwidth = GridBagConstraints.REMAINDER;
67     addComponent( buttons[ 3 ] );
68
```

```
69    // buttons[4] -- weightx and weighty are 1: fill is BOTH
70    constraints.gridwidth = GridBagConstraints.RELATIVE;
71    addComponent( buttons[ 4 ] );
72
73    // list -- weightx and weighty are 1: fill is BOTH
74    constraints.gridwidth = GridBagConstraints.REMAINDER;
75    addComponent( list );
76 } // end GridBagFrame2 constructor
77
78    // add a component to the container
79    private void addComponent( Component component )
80    {
81        layout.setConstraints( component, constraints );
82        add( component ); // add component
83    } // end method addComponent
84 } // end class GridBagFrame2
```

## Fig. 25.23 | GridBagConstraints constants RELATIVE and REMAINDER. (Part 3 of 3.)

```
1  // Fig. 25.24: GridBagDemo2.java
2  // Demonstrating GridBagLayout constants.
3  import javax.swing.JFrame;
4
5  public class GridBagDemo2
6  {
7      public static void main( String[] args )
8      {
9          GridBagFrame2 gridBagFrame = new GridBagFrame2();
10         gridBagFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
11         gridBagFrame.setSize( 300, 200 ); // set frame size
12         gridBagFrame.setVisible( true ); // display frame
13     } // end main
14  } // end class GridBagDemo2
```

![](img/009e962758dcc71dbc43a493362e6dc0_1076_0.png)

## Fig. 25.24 | Test class for GridBagDemo2.

第 21–22 行创建 GridBagLayout 并用它设置 JFrame 的布局管理器。放置在 GridBagLayout 中的组件在第 27–38 行创建——它们是一个 JComboBox、一个 JTextField、一个 JList 和五个 JButtons。

JTextField 首先被添加（第 41–45 行）。weightx 和 weighty 值都设置为 1。fill 变量设置为 BOTH。第 44 行指定 JTextField 是该行的最后一个组件。JTextField 通过调用我们的实用方法 addComponent（在第 79–83 行声明）添加到内容窗格。方法 addComponent 接受一个 Component 参数并使用 GridBagLayout 方法 setConstraints 为 Component 设置约束。方法 add 将组件附加到内容窗格。

JButton buttons[ 0 ]（第 48–49 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。因为 buttons[ 0 ] 不是该行最后两个组件之一，所以它被赋予 gridwidth 为 1，因此将占用一列。该 JButton 通过调用实用方法 addComponent 添加到内容窗格。

JButton buttons[ 1 ]（第 52–53 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。第 52 行指定 JButton 应相对于前一个组件放置。该按钮通过调用 addComponent 添加到 JFrame。

JButton buttons[ 2 ]（第 56–57 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。此 JButton 是该行的最后一个组件，因此使用 REMAINDER。该 JButton 通过调用 addComponent 添加到内容窗格。

JComboBox（第 60–62 行）的 weightx 为 1，weighty 为 0。JComboBox 不会垂直增长。JComboBox 是该行中唯一的组件，因此使用 REMAINDER。JComboBox 通过调用 addComponent 添加到内容窗格。

JButton buttons[ 3 ]（第 65–67 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。此 JButton 是该行中唯一的组件，因此使用 REMAINDER。该 JButton 通过调用 addComponent 添加到内容窗格。

JButton buttons[ 4 ]（第 70–71 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。此 JButton 是该行的倒数第二个组件，因此使用 RELATIVE。该 JButton 通过调用 addComponent 添加到内容窗格。

JList（第 74–75 行）的 weightx 和 weighty 值为 1。fill 变量为 BOTH。JList 通过调用 addComponent 添加到内容窗格。

## 25.10 总结

本章完成了我们对 GUI 的介绍。在本章中，我们讨论了额外的 GUI 主题，例如菜单、滑块、弹出菜单、多文档界面、选项卡窗格和 Java 的可插拔外观。所有这些组件都可以添加到现有应用程序中以使其更易于使用和理解。我们还介绍了用于组织和调整 GUI 组件大小的额外布局管理器。在下一章中，您将学习多线程，它允许您指定应用程序应同时执行多个任务。

## 摘要

## Section 25.2 JSlider

- JSliders 使您能够从一系列整数值中进行选择。它们可以显示主要和次要刻度标记，以及刻度标记的标签（p. 1001）。它们还支持吸附到刻度（p. 1001）——将拇指（p. 1001）定位在两个刻度标记之间会使其吸附到最近的刻度标记。

- JSliders（p. 1001）具有水平或垂直方向。对于水平 JSlider，最小值在最左侧，最大值在最右侧。对于垂直 JSlider，最小值在最底部，最大值在最顶部。拇指的位置表示 JSlider 的当前值。JSlider 类的方法 getValue（p. 1005）返回拇指的当前位置。

