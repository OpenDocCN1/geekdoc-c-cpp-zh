
## 程序清单 7.19

```
//***************************************************************************
// IntroPanel.java          Author: Lewis/Loftus
//
// Represents the introduction panel for the LayoutDemo program.
//***************************************************************************

import java.awt.*;
import javax.swing.*;

public class IntroPanel extends JPanel
{
    //-------------------------------------------------------------
    // Sets up this panel with two labels.
    //-------------------------------------------------------------
    public IntroPanel()
    {
        setBackground (Color.green);

        JLabel l1 = new JLabel ("Layout Manager Demonstration");
        JLabel l2 = new JLabel ("Choose a tab to see an example of " +
                                "a layout manager.");

        add (l1);
        add (l2);
    }
}
```

### 显示

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_380_0.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_381_0.png)

## 图 7.7 流式布局在一行中尽可能多地放置组件

## 程序清单 7.20

```
//************************************************************************
// FlowPanel.java        Author: Lewis/Loftus
//
// Represents the panel in the LayoutDemo program that demonstrates
// the flow layout manager.
//************************************************************************

import java.awt.*;
import javax.swing.*;

public class FlowPanel extends JPanel
{
    //-------------------------------------------------------------
    // Sets up this panel with some buttons to show how flow layout
    // affects their position.
    //-------------------------------------------------------------
    public FlowPanel ()
    {
        setLayout (new FlowLayout());

        setBackground (Color.green);

        JButton b1 = new JButton ("BUTTON 1");
        JButton b2 = new JButton ("BUTTON 2");
        JButton b3 = new JButton ("BUTTON 3");
        JButton b4 = new JButton ("BUTTON 4");
        JButton b5 = new JButton ("BUTTON 5");
```

## 程序清单 7.20

（续）

```
add (b1);
add (b2);
add (b3);
add (b4);
add (b5);
}
}
```

### 显示

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_382_0.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_382_1.png)

（尽管在这种情况下这一步并不是必需的，因为 JPanel 默认使用流式布局）。然后创建按钮并将它们添加到面板中。

每个按钮的大小都足以容纳其上的标签。正如我们前面提到的，流式布局会尽可能多地将这些按钮放在面板的一行中，然后开始把组件放到另一行。当框架变宽时（例如用鼠标拖动右下角），面板也会随之变大，一行中可以容纳更多按钮。当框架调整大小时，会调用布局管理器并自动重新组织这些组件。注意，默认情况下，每一行中的组件都会在窗口内居中。

FlowLayout 类的构造函数被重载，允许程序员定制布局管理器的特性。在每一行中，组件要么居中，要么左对齐，要么右对齐，默认是居中。创建布局管理器时，还可以指定组件之间的水平和垂直间距。FlowLayout 类还提供了在布局管理器创建之后设置对齐方式和间距大小的方法。

## 边界布局

边界布局有五个可以添加组件的区域：北部、南部、东部、西部和中部区域。这些区域彼此之间具有特定的位置关系，如图 7.8 所示。

四个外部区域会按需扩展，以容纳其中所含的组件。如果没有向北、南、东、西区域添加组件，这些区域不会在整体布局中占据任何空间。中部区域会扩展以填满所有可用空间。

根据系统功能的不同，特定容器可能只使用其中几个区域。例如，一个程序可能只使用中部、南部和西部区域。这种灵活性使得边界布局成为一种非常实用的布局管理器。

对于由边界布局管理的容器，其 `add` 方法的第一个参数是要添加的组件，第二个参数指明要添加到的区域。区域通过使用 `BorderLayout` 类中定义的常量来指定。程序清单 7.21 显示了 `LayoutDemo` 程序用来演示边界布局的面板。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_383_0.png)

### 图 7.8 边界布局将组件组织在五个区域中

## 程序清单 7.21

```
//***************************************************************************
// BorderPanel.java        Author: Lewis/Loftus
//
// Represents the panel in the LayoutDemo program that demonstrates
// the border layout manager.
//***************************************************************************

import java.awt.*;
import javax.swing.*;

public class BorderPanel extends JPanel
{
    //-------------------------------------------------------------
    // Sets up this panel with a button in each area of a border
    // layout to show how it affects their position, shape, and size.
    //-------------------------------------------------------------
    public BorderPanel()
    {
        setLayout (new BorderLayout());

        setBackground (Color.green);

        JButton b1 = new JButton ("BUTTON 1");
        JButton b2 = new JButton ("BUTTON 2");
        JButton b3 = new JButton ("BUTTON 3");
        JButton b4 = new JButton ("BUTTON 4");
        JButton b5 = new JButton ("BUTTON 5");

        add (b1, BorderLayout.CENTER);
        add (b2, BorderLayout.NORTH);
        add (b3, BorderLayout.SOUTH);
        add (b4, BorderLayout.EAST);
        add (b5, BorderLayout.WEST);
    }
}
```

## 程序清单 7.21

（续）

### 显示

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_385_0.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_385_1.png)

在 `BorderPanel` 类的构造函数中，面板的布局管理器被显式设置为边界布局。然后创建按钮并将它们添加到特定的面板区域中。默认情况下，每个按钮都被设置为宽度足以容纳其标签，高度足以填满它被分配到的区域。当框架（以及面板）调整大小时，每个按钮的大小会按需调整，中部区域的按钮会填满所有未使用的空间。

边界布局中的每个区域只显示一个组件。也就是说，在给定的边界布局中，每个区域只能添加一个组件。一个常见错误是向边界布局的某个区域添加两个组件，这时先添加的组件会被后添加的组件替换，容器显示时只会看到后添加的那个组件。要向边界布局的某个区域添加多个组件，可以先将这些组件添加到另一个容器（如 `JPanel`）中，然后再将该面板添加到该区域。

注意，尽管用于显示按钮的面板具有绿色背景，但在程序清单 7.21 的显示中看不到任何绿色。默认情况下，边界布局的区域之间没有水平或垂直间距。这些间距可以通过重载的构造函数或 `BorderLayout` 类的显式方法来设置。如果增大间距，底层面板就会透出来。

## 网格布局

网格布局以由行和列组成的矩形网格形式呈现容器的组件。每个网格单元放置一个组件，并且所有单元的大小相同。图 7.9 展示了网格布局的总体组织结构。

网格布局的行数和列数是在创建布局管理器时通过构造函数的参数确定的。程序清单 7.22 中的类显示了 `LayoutDemo` 程序用来演示网格布局的面板。它指定该面板应使用两行三列的网格进行管理。

随着按钮被添加到容器中，它们（默认情况下）按从左到右、从上到下的顺序填满网格。除了按添加到容器中的顺序外，无法将组件显式分配到网格中的特定位置。

每个单元的大小由容器的整体大小决定。当容器调整大小时，所有单元都会按比例改变大小以填满容器。

如果用于指定行数或列数的值为零，则该维度上的网格会根据添加到容器中的组件数量按需扩展。行数和列数的值不能同时为零。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_386_0.png)

### 图 7.9 网格布局创建由等大小单元格组成的矩形网格
