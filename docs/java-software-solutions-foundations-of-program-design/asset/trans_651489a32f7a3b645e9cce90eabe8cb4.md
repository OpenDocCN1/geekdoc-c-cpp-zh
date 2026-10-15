

# LISTING 5.11 continued

```
import java.util.ArrayList;

public class Beatles
{
    //------------------------------------------------------------
    // Stores and modifies a list of band members.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        ArrayList<String> band = new ArrayList<String>();

        band.add ("Paul");
        band.add ("Pete");
        band.add ("John");
        band.add ("George");

        System.out.println (band);
        int location = band.indexOf ("Pete");
        band.remove (location);

        System.out.println (band);
        System.out.println ("At index 1: " + band.get(1));
        band.add (2, "Ringo");

        System.out.println ("Size of the band: " + band.size());
        int index = 0;
        while (index < band.size())
        {
            System.out.println (band.get(index));
            index++;
        }
    }
}
```

# OUTPUT

[Paul, Pete, John, George]
[Paul, John, George]
At index 1: John
Size of the band: 4
Paul
John
Ringo
George

# LISTING 5.12

```
//*******************************************************************
// LeftRight.java      Author: Lewis/Loftus
//
// Demonstrates the use of one listener for multiple buttons.
//*******************************************************************

import javax.swing.JFrame;

public class LeftRight
{
    //-------------------------------------------------------------
    // Creates the main program frame.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Left Right");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        frame.getContentPane().add(new LeftRightPanel());

        frame.pack();
        frame.setVisible(true);
    }
}
```

# DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_276_0.png)

# LISTING 5.13

```
//************************************************************************
//  LeftRightPanel.java      Author: Lewis/Loftus
//
//  Demonstrates the use of one listener for multiple buttons.
//************************************************************************

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class LeftRightPanel extends JPanel
{
    private JButton left, right;
    private JLabel label;
    private JPanel buttonPanel;

    //-------------------------------------------------------------
    //  Constructor: Sets up the GUI.
    //-------------------------------------------------------------
    public LeftRightPanel ()
    {
        left = new JButton ("Left");
        right = new JButton ("Right");

        ButtonListener listener = new ButtonListener();
        left.addActionListener (listener);
        right.addActionListener (listener);

        label = new JLabel ("Push a button");

        buttonPanel = new JPanel();
        buttonPanel.setPreferredSize (new Dimension(200, 40));
        buttonPanel.setBackground (Color.blue);
        buttonPanel.add (left);
        buttonPanel.add (right);

        setPreferredSize (new Dimension(200, 80));
        setBackground (Color.cyan);
        add (label);
        add (buttonPanel);
    }
```

# LISTING 5.13 continued

```
//****************************************************************
// Represents a listener for both buttons.
//****************************************************************
private class ButtonListener implements ActionListener
{
    //---------------------------------------------------------------
    // Determines which button was pressed and sets the label
    // text accordingly.
    //---------------------------------------------------------------
    public void actionPerformed(ActionEvent event)
    {
        if (event.getSource() == left)
            label.setText("Left");
        else
            label.setText("Right");
    }
}
```

我们本可以创建两个独立的监听器类，一个监听左按钮，另一个监听右按钮。在这种情况下，`actionPerformed` 方法就不需要确定事件的来源。是否使用多个监听器或在事件发生时确定事件来源，是一个设计决策，应根据具体情况做出。

请注意，两个按钮都放在名为 `buttonPanel` 的同一个面板上，该面板与 `LeftRightPanel` 类所表示的面板是分开的。通过将两个按钮放在一个面板上，我们可以保证它们之间的视觉关系，即使在以各种方式调整框架大小时也是如此。对于标有 Left 和 Right 的按钮来说，这可能很重要。

## 5.8 复选框和单选按钮

按 `JButton` 类定义的推送按钮，只是我们在 Java GUI 中可以使用的一种按钮。另两种是复选框和单选按钮。让我们详细了解它们。

### 复选框

复选框是一种可以使用鼠标切换开/关的按钮，表示某个布尔条件被设置或未设置。例如，一个标记为 Collate 的复选框可能用于指示打印作业的输出是否应整理。虽然你可能有一组复选框表示一组选项，但每个复选框都是独立操作的。也就是说，每个复选框都可以设置为开或关，一个的状态不会影响其他。

程序在 Listing 5.14 中显示了两个复选框和一个标签。复选框决定标签的文本是以粗体、斜体、两者兼有还是两者皆无显示。粗体和斜体的任何组合都是有效的。例如，两个复选框都可能被选中（打开），在这种情况下，文本将同时以粗体和斜体显示。如果两者都未选中，标签的文本将以普通样式显示。

StyleOptions 程序的 GUI 由 Listing 5.15 中所示的 `StyleOptionsPanel` 类实现。复选框由 `JCheckBox` 类表示。当复选框从选中（已勾选）状态更改为未选中（未勾选）状态，或反之亦然时，它会生成一个项目事件。`ItemListener` 接口包含一个名为 `itemStateChanged` 的单一方法。在本例中，我们使用同一个监听器对象来处理两个复选框。

# LISTING 5.14

```
//****************************************************************
//  StyleOptions.java      Author: Lewis/Loftus
//
//  Demonstrates the use of check boxes.
//****************************************************************

import javax.swing.JFrame;

public class StyleOptions
{
    //-------------------------------------------------------------
    // Creates and presents the program frame.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Style Options");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        StyleOptionsPanel panel = new StyleOptionsPanel();
        frame.getContentPane().add (panel);

        frame.pack();
        frame.setVisible(true);
    }
}
```

# LISTING 5.14 continued

# DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_280_0.png)

# LISTING 5.15

```
//****************************************************************
//  StyleOptionsPanel.java        Author: Lewis/Loftus
//
//  Demonstrates the use of check boxes.
//****************************************************************

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class StyleOptionsPanel extends JPanel
{
    private JLabel saying;
    private JCheckBox bold, italic;

    //---------------------------------------------------------------
    //  Sets up a panel with a label and some check boxes that
    //  control the style of the label's font.
    //---------------------------------------------------------------
    public StyleOptionsPanel()
    {
        saying = new JLabel ("Say it with style!");
        saying.setFont (new Font ("Helvetica", Font.PLAIN, 36));

        bold = new JCheckBox ("Bold");
        bold.setBackground (Color.cyan);

