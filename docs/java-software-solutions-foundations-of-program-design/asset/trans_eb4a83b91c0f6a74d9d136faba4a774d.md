

## LISTING 11.13 continued

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_598_0.png)

滚动窗格可以在容器的右侧有一个垂直滚动条，以及在容器的底部有一个水平滚动条。对于这两者，程序员可以指定滚动条是始终使用、从不使用，或根据需要使用以查看底层组件。默认情况下，垂直和水平滚动条均按需使用。TransiMap 程序依赖于这些默认值，并且由于图像在高度和宽度上都太大，因此两个滚动条都会出现。

要移动滚动条，用户可以点击并拖动滚动条中的方块，即表示其当前位置的旋钮（在该维度上：上/下或右/左）。或者，用户可以点击旋钮右侧或左侧的条，或点击滚动条两端的箭头来调整位置。程序员可以确定这些操作中的每一个如何改变显示区域。

请注意，使用滚动窗格以这种方式不需要设置任何事件监听器。滚动窗格会自动响应其滚动条的调整。

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

+ SR 11.27 描述滚动窗格上滚动条的使用。
+ SR 11.28 如果将 TransitMap 程序中 Dimension 构造函数的第一个参数更改为 1000 会发生什么？解释。

## 11.10 Split Panes

分割窗格是一个容器，它通过可移动的分隔条显示两个组件。根据分割窗格的设置方式，两个组件要么并排显示，要么一个在另一个之上，如图 11.3 所示。在 Java 中，我们可以使用 JSplitPane 类创建分割窗格。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_599_0.png)

FIGURE 11.3 The configurations of a split pane

该面板包含列表和要显示的图像的标签并排放置。对 setOneTouchExpandable 方法的调用使得分割窗格的分隔条显示箭头，允许用户通过一次鼠标点击将窗格向一侧或另一侧展开。

## LISTING 11.14

```
//****************************************************************
//  PickImage.java      Author: Lewis/Loftus
//
//  Demonstrates the use of a split pane and a list.
//****************************************************************

import java.awt.*;
import javax.swing.*;

public class PickImage
{
    //-------------------------------------------------------------
    //  Creates and displays a frame containing a split pane. The
    //  user selects an image name from the list to be displayed.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Pick Image");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        JLabel imageLabel = new JLabel();
        JPanel imagePanel = new JPanel();
        imagePanel.add (imageLabel);
        imagePanel.setBackground (Color.white);

        ListPanel imageList = new ListPanel (imageLabel);

        JSplitPane sp = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT,
                                    imageList, imagePanel);

        sp.setOneTouchExpandable (true);

        frame.getContentPane().add (sp);
        frame.pack();
        frame.setVisible(true);
    }
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_602_0.png)

Listing 11.15 中显示的 ListPanel 类定义了包含文件名列表的面板。我们使用列表组件，即 JList 类，来显示文件名列表。列表内容被设置为 String 对象的数组，并传递给 JList 构造函数。

```
//******************************
// ListPanel.java Author: Lewis/Loftus
// Represents the list of images for the PickImage program.
//******************************
import java.awt.*;
import javax.swing.*;
import javax.swing.event.*;
public class ListPanel extends JPanel
{
    private JLabel label;
```

## LISTING 11.15 continued

```
private JList list;

//------------------------------------------------------------
// Loads the list of image names into the list.
//------------------------------------------------------------
public ListPanel (JLabel imageLabel)
{
    label = imageLabel;

    String[] fileNames = { "circuit.gif",
                           "duke.gif",
                           "hammock.gif",
                           "justin.jpg",
                           "kayla.jpg",
                           "tiger.jpg",
                           "toucan.gif",
                           "worldmap.gif" };

    list = new JList (fileNames);
    list.addListSelectionListener (new ListListener());
    list.setSelectionMode (ListSelectionModel.SINGLE_SELECTION);

    add (list);
    setBackground (Color.white);
}

//****************************************************************
// Represents the listener for the list of images.
//****************************************************************
private class ListListener implements ListSelectionListener
{
    public void valueChanged (ListSelectionEvent event)
    {
        if (list.isSelectionEmpty())
            label.setIcon (null);
        else
        {
            String fileName = (String)list.getSelectedValue();
            ImageIcon image = new ImageIcon (fileName);
            label.setIcon (image);
        }
    }
}
```

通常，JList 组件中的所有选项都是可见的。当用户使用鼠标选择一个项目时，它会被高亮显示。当选择新项目时，先前选择的项目会自动取消高亮。

JList 的内容可以使用传递给构造函数的对象数组来指定。JList 类的方法用于以各种方式管理列表，包括检索当前选中的项目。

请注意组合框（在第 11.8 节中描述）和 JList 对象之间的相似性和差异。两者都允许用户从一组选择中选择一个项目。然而，列表中的选择始终显示，当前选择被高亮显示，而组合框只有在用户用鼠标按下它时才显示其选项。组合框中始终显示的唯一项目是当前选择。

每当列表的当前选择发生变化时，JList 对象都会生成一个 *list selection event*。ListSelectionListener 接口包含一个名为 valueChanged 的方法。在此程序中，名为 ListListener 的私有内部类定义了文件名列表的监听器。

监听器的 valueChanged 方法调用 JList 对象的 isSelectionEmpty 方法来确定当前是否有任何值被选中。如果没有，则标签的图标被设置为 `null`。如果有，则使用 getSelectedValue 方法获取文件名。然后创建相应的图像图标并在标签中显示。

JList 对象可以设置为允许同时选择多个项目。*list selection mode* 可以是三种选项之一，如图 11.4 中的表格所示。

列表选择模式由 ListSelectionModel 对象定义。默认情况下，列表允许多区间选择。使用 ListSelectionModel 类中定义的常量调用 setSelectionMode 方法将显式设置列表选择模式。

在 PickImage 程序中，我们将列表选择模式设置为单选，因为一次只能显示一个图像。然而，即使多个

| List Selection Mode | Description |
|---|---|
| Single Selection | Only one item can be selected at a time. |
| Single Interval Selection | Multiple, contiguous items can be selected at a time. |
| Multiple Interval Selection | Any combination of items can be selected. |

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_604_0.png)

