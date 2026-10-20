

变量 **gridwidth** 指定组件占用的列数。JComboBox 占用两列。变量 **gridheight** 指定组件占用的行数。图 25.18 左侧的 JTextArea 占用三行。

变量 **weightx** 指定在 GridBagLayout 中容器被调整大小时如何将额外的水平空间分配给网格槽。零值表示网格槽本身在水平方向上不会增长。然而，如果组件跨越包含具有非零 weightx 值的组件的列，则具有零 weightx 值的组件将在与该列中其他组件相同的比例下水平增长。这是因为每个组件必须保持在其最初放置的同一行和列中。

变量 **weighty** 指定在 GridBagLayout 中容器被调整大小时如何将额外的垂直空间分配给网格槽。零值表示网格槽本身在垂直方向上不会增长。然而，如果组件跨越包含具有非零 weighty 值的组件的行，则具有零 weighty 值的组件将在与同一行中其他组件相同的比例下垂直增长。

在图 25.18 中，weighty 和 weightx 的效果在容器被调整大小并且有额外空间可用之前很难看到。具有较大权重值的组件比具有较小权重值的组件占用更多的额外空间。

组件应被赋予非零正权重值——否则它们会在容器的中间“挤在一起”。图 25.20 显示了图 25.18 的 GUI，所有权重都设置为零。

![](img/009e962758dcc71dbc43a493362e6dc0_1070_0.png)

**图 25.20** | 权重设置为零的 GridBagLayout。

图 25.21–25.22 中的应用程序使用 GridBagLayout 布局管理器来排列图 25.18 中 GUI 的组件。该应用程序除了演示如何使用 GridBagLayout 外什么也不做。

```
// Fig. 25.21: GridBagFrame.java
// Demonstrating GridBagLayout.
import java.awt.GridBagLayout;
import java.awt.GridBagConstraints;
import java.awt.Component;
import javax.swing.JFrame;
import javax.swing.JTextArea;
import javax.swing.JTextField;
```

**图 25.21** | GridBagLayout 布局管理器。（第 1 部分，共 3 部分。）

```
9 import javax.swing.JButton;
10 import javax.swing.JComboBox;

public class GridBagFrame extends JFrame
{
    private GridBagLayout layout; // layout of this frame
    private GridBagConstraints constraints; // constraints of this layout

    // set up GUI
    public GridBagFrame()
    {
        super( "GridBagLayout" );
        layout = new GridBagLayout();
        setLayout( layout ); // set frame layout
        constraints = new GridBagConstraints(); // instantiate constraints

        // create GUI components
        JTextArea textArea1 = new JTextArea( "TextArea1", 5, 10 );
        JTextArea textArea2 = new JTextArea( "TextArea2", 2, 2 );

        String[] names = { "Iron", "Steel", "Brass" };
        JComboBox comboBox = new JComboBox( names );

        JTextField textField = new JTextField( "TextField" );
        JButton button1 = new JButton( "Button 1" );
        JButton button2 = new JButton( "Button 2" );
        JButton button3 = new JButton( "Button 3" );

        // weightx and weighty for textArea1 are both 0: the default
        // anchor for all components is CENTER: the default
        constraints.fill = GridBagConstraints.BOTH;
        addComponent( textArea1, 0, 0, 1, 3 );

        // weightx and weighty for button1 are both 0: the default
        constraints.fill = GridBagConstraints.HORIZONTAL;
        addComponent( button1, 0, 1, 2, 1 );

        // weightx and weighty for comboBox are both 0: the default
        // fill is HORIZONTAL
        addComponent( comboBox, 2, 1, 2, 1 );

        // button2
        constraints.weightx = 1000;  // can grow wider
        constraints.weighty = 1;     // can grow taller
        constraints.fill = GridBagConstraints.BOTH;
        addComponent( button2, 1, 1, 1, 1 );

        // fill is BOTH for button3
        constraints.weightx = 0;
        constraints.weighty = 0;
        addComponent( button3, 1, 2, 1, 1 );
```

```
// weightx and weighty for textField are both 0, fill is BOTH
addComponent( textField, 3, 0, 2, 1 );

// weightx and weighty for textArea2 are both 0, fill is BOTH
addComponent( textArea2, 3, 2, 1, 1 );
} // end GridBagFrame constructor

// method to set constraints on
private void addComponent( Component component,
    int row, int column, int width, int height )
{
    constraints.gridx = column; // set gridx
    constraints.gridy = row; // set gridy
    constraints.gridwidth = width; // set gridwidth
    constraints.gridheight = height; // set gridheight
    layout.setConstraints( component, constraints ); // set constraints
    add( component ); // add component
} // end method addComponent
} // end class GridBagFrame
```

图 25.21 | GridBagLayout 布局管理器。（第 3 部分，共 3 部分。）

```
// Fig. 25.22: GridBagDemo.java
// Demonstrating GridBagLayout.
import javax.swing.JFrame;

public class GridBagDemo
{
    public static void main( String[] args )
    {
        GridBagFrame gridBagFrame = new GridBagFrame();
        gridBagFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        gridBagFrame.setSize( 300, 150 ); // set frame size
        gridBagFrame.setVisible( true ); // display frame
    } // end main
} // end class GridBagDemo
```

![](img/009e962758dcc71dbc43a493362e6dc0_1072_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_1072_1.png)

图 25.22 | GridBagFrame 的测试类。（第 1 部分，共 2 部分。）

![](img/009e962758dcc71dbc43a493362e6dc0_1073_0.png)

# 图 25.22 | GridBagFrame 的测试类。（第 2 部分，共 2 部分。）

GUI 包含三个 JButtons、两个 JTextAreas、一个 JComboBox 和一个 JTextField。布局管理器是 GridBagLayout。第 21–22 行创建 GridBagLayout 对象并将布局管理器设置为 JFrame 的 layout。第 23 行创建用于确定网格中每个组件的位置和大小的 GridBagConstraints 对象。第 26–35 行创建将添加到内容窗格的每个 GUI 组件。

第 39–40 行配置 JTextArea textArea1 并将其添加到内容窗格。constraints 中未指定 weightx 和 weighty 值，因此默认值均为零。因此，即使有可用空间，JTextArea 也不会自行调整大小。然而，它跨越多行，因此垂直尺寸受 JButtons button2 和 button3 的 weighty 值影响。当任一按钮基于其 weighty 值垂直调整大小时，JTextArea 也会被调整大小。

第 39 行将 constraints 中的变量 fill 设置为 GridBagConstraints.BOTH，导致 JTextArea 总是填充网格中分配给它的整个区域。constraints 中未指定 anchor 值，因此使用默认的 CENTER。我们在此应用程序中不使用变量 anchor，因此所有组件都将使用默认值。第 40 行调用我们的实用方法 addComponent（在第 69–78 行声明）。JTextArea 对象、行、列、要跨越的列数和要跨越的行数作为参数传递。

JButton button1 是下一个添加的组件（第 43–44 行）。默认情况下，weightx 和 weighty 值仍为零。fill 变量设置为 HORIZONTAL——组件将始终在水平方向上填充其区域。垂直方向不填充。weighty 值为零，因此按钮只有在同一行中存在具有非零 weighty 值的其他组件时才会变高。JButton button1 位于第 0 行、第 1 列。占用一行和两列。

JComboBox comboBox 是下一个添加的组件（第 48 行）。默认情况下，weightx 和 weighty 值为零，fill 变量设置为 HORIZONTAL。JComboBox 按钮只会在水平方向上增长。weightx、weighty 和 fill 变量在 constraints 中保留其设置的值，直到它们被更改。JComboBox 按钮放置在第 2 行、第 1 列。占用一行和两列。

JButton button2 是下一个添加的组件（第 51–54 行）。它被赋予 weightx 值为 1000 和 weighty 值为 1。按钮占用的区域能够在垂直和水平方向上增长。fill 变量设置为 BOTH，指定按钮将始终填充整个区域。当窗口被调整大小时，button2 将会增长。按钮放置在第 1 行、第 1 列。占用一行和一列。

