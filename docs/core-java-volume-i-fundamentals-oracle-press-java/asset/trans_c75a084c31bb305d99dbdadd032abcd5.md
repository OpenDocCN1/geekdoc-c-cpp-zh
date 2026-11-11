
```java
 * selecting font
 9    * attributes.
10    */
11 public class CheckBoxFrame extends JFrame
12 {
13    private JLabel label;
14    private JCheckBox bold;
15    private JCheckBox italic;
16    private static final int FONTSIZE = 24;
17
18    public CheckBoxFrame()
19    {
20       // add the sample text label
21
22       label = new JLabel("The quick brown fox jumps over the lazy dog.");
23       label.setFont(new Font("Serif", Font.BOLD, FONTSIZE));
24       add(label, BorderLayout.CENTER);
25
26       // this listener sets the font attribute of
27       // the label to the check box state
28
29       ActionListener listener = event ->
30       {
31          int mode = 0;
32          if (bold.isSelected()) mode += Font.BOLD;
33          if (italic.isSelected()) mode += Font.ITALIC;
34          label.setFont(new Font("Serif", mode, FONTSIZE));
35       };
36
37       // add the check boxes
38       var buttonPanel = new JPanel();
39
40       bold = new JCheckBox("Bold");
41       bold.addActionListener(listener);
42       bold.setSelected(true);
43       buttonPanel.add(bold);
44
45       italic = new JCheckBox("Italic");
46       italic.addActionListener(listener);
47       buttonPanel.add(italic);
48
49       add(buttonPanel, BorderLayout.SOUTH);
50       pack();
51    }
52 }
```

### javax.swing.JCheckBox 1.2

- `JCheckBox(String label)`
- `JCheckBox(String label, Icon icon)`  
  构造一个初始未被选中的复选框。
- `JCheckBox(String label, boolean state)`  
  使用给定的标签和初始状态构造一个复选框。
- `boolean isSelected()`
- `void setSelected(boolean state)`  
  获取或设置复选框的选中状态。

### 11.4.2 单选按钮

在之前的示例中，用户可以选择两个复选框中的任意一个、两个都选，或者两个都不选。但在许多情况下，我们希望用户只能从几个选项中选择一个。每当选中另一个选项时，之前选中的选项会自动取消选中。这样的一组选项通常被称为*单选按钮组*，因为这些按钮的工作方式类似于收音机上的电台选择按钮。当你按下一个按钮时，之前按下的按钮会自动弹起。图11.13展示了一个典型示例。我们允许用户从“小”“中”“大”“特大”这几个选项中选择字体大小——但当然，每次只能选中一个大小。

![](img/0e7b74ef51a065c077b42cd87b362288_941_0.png)

**图11.13** 单选按钮组

在Swing中实现单选按钮组非常简单。你需要为每一组按钮构造一个类型为`ButtonGroup`的对象，然后将类型为`JRadioButton`的对象添加到该按钮组中。按钮组对象负责在点击新按钮时取消选中之前被选中的按钮。

```
var group = new ButtonGroup();

var smallButton = new JRadioButton("Small", false);
group.add(smallButton);

var mediumButton = new JRadioButton("Medium", true);
group.add(mediumButton);
. . .
```

构造函数的第二个参数为`true`表示该按钮应在初始时被选中，其余按钮则为`false`。请注意，按钮组只控制按钮的*行为*；如果你需要从布局角度对按钮进行分组，还需要将它们添加到一个容器中，例如`JPanel`。

如果再看一下图11.12和图11.13，你会注意到单选按钮的外观与复选框不同。复选框是方形的，选中时会出现一个对勾；单选按钮是圆形的，选中时会出现一个圆点。

单选按钮的事件通知机制与其他任何按钮相同。当用户选中一个单选按钮时，该按钮会生成一个动作事件。在我们的示例程序中，我们定义了一个动作监听器，将字体大小设置为特定值：

```
ActionListener listener = event ->
    label.setFont(new Font("Serif", Font.PLAIN, size));
```

将这个监听器的设置与复选框示例中的设置进行比较。每个单选按钮都获得一个不同的监听器对象。每个监听器对象都确切地知道自己需要做什么——将字体大小设置为特定值。对于复选框，我们使用了不同的方法：两个复选框使用同一个动作监听器，它调用一个方法来检查两个复选框的当前状态。

我们在这里能采用相同的方法吗？我们可以使用一个单一的监听器，按如下方式计算大小：

```
if (smallButton.isSelected()) size = 8;
else if (mediumButton.isSelected()) size = 12;
. . .
```

然而，我们更倾向于使用单独的动作监听器对象，因为它们能将大小值与按钮更紧密地关联起来。

![](img/0e7b74ef51a065c077b42cd87b362288_942_0.png)

**注意：**

如果你有一组单选按钮，你就知道其中只有一个会被选中。如果能快速找出是哪一个，而不必查询组中的所有按钮，那将会很方便。`ButtonGroup`对象控制着所有按钮，因此如果这个对象能提供对选中按钮的引用，那将会很方便。实际上，`ButtonGroup`类确实有一个`getSelection`方法，但该方法并不会返回被选中的单选按钮。相反，它返回一个指向按钮所附带模型的`ButtonModel`引用。遗憾的是，`ButtonModel`的方法中没有一个是有用的。`ButtonModel`接口从`ItemSelectable`接口继承了一个`getSelectedObjects`方法，但该方法很无用，返回的是`null`。`getActionCommand`方法看起来很有希望，因为单选按钮的“动作命令”就是它的文本标签。但它的模型的动作命令是`null`。只有当你使用`setActionCommand`方法显式地设置所有单选按钮的动作命令时，模型的动作命令值才会被设置。这时，你就可以通过`buttonGroup.getSelection().getActionCommand()`获取当前选中按钮的动作命令了。

`Listing 11.3` 是字体大小选择的完整程序，它使用了一组单选按钮。

### Listing 11.3 radioButton/RadioButtonFrame.java

```java
 1 package radioButton;
 2
 3 import java.awt.*;
 4 import java.awt.event.*;
 5 import javax.swing.*;
 6
 7 /**
 8  * A frame with a sample text label and radio buttons for selecting font sizes.
 9  */
10 public class RadioButtonFrame extends JFrame
11 {
12    private JPanel buttonPanel;
13    private ButtonGroup group;
14    private JLabel label;
15    private static final int DEFAULT_SIZE = 36;
16
17    public RadioButtonFrame()
18    {
19       // add the sample text label
20
21       label = new JLabel("The quick brown fox jumps over the lazy dog.");
       label.setFont(new Font("Serif", Font.PLAIN, DEFAULT_SIZE));
       add(label, BorderLayout.CENTER);

       // add the radio buttons

       buttonPanel = new JPanel();
       group = new ButtonGroup();

       addRadioButton("Small", 8);
       addRadioButton("Medium", 12);
       addRadioButton("Large", 18);
       addRadioButton("Extra large", 36);

       add(buttonPanel, BorderLayout.SOUTH);
       pack();
    }

    /**
     * Adds a radio button that sets the font size of the sample text.
     * @param name the string to appear on the button
     * @param size the font size that this button sets
     */
    public void addRadioButton(String name, int size)
    {
        boolean selected = size == DEFAULT_SIZE;
        var button = new JRadioButton(name, selected);
        group.add(button);
        buttonPanel.add(button);

        // this listener sets the label font size

        ActionListener listener = event -> label.setFont(new Font("Serif", Font.PLAIN, size));

        button.addActionListener(listener);
    }
}
```

### 11.4.3 边框

如果在窗口中有多组单选按钮，你会希望以视觉方式指示哪些按钮属于同一组。为此，Swing提供了一组有用的*边框*。你可以将边框应用于任何继承自`JComponent`的组件。最常见的用法是在面板周围放置边框，并用其他用户界面元素（如单选按钮）填充该面板。

你可以从相当多的边框中进行选择，但所有边框都需要遵循相同的步骤。

1. 调用`BorderFactory`的静态方法来创建边框。你可以从以下样式中选择（参见[图11.14](#figure-1114)）：
   - 低凹陷斜面
   - 高凸起斜面
   - 蚀刻
   - 直线
   - 哑光
   - 空（仅在组件周围创建一些空白空间）

![](img/0e7b74ef51a065c077b42cd87b362288_946_0.png)

**图11.14** 测试边框类型

2. 如果你愿意，可以通过将边框传递给`BorderFactory.createTitledBorder`来为边框添加标题。

