
8  import javax.swing.JFrame;
9  import javax.swing.JLabel;
10 import javax.swing.JPanel;
11 
12 public class MouseTrackerFrame extends JFrame
13 {
14     private JPanel mousePanel; // panel in which mouse events will occur
15     private JLabel statusBar; // label that displays event information
16 
17     // MouseTrackerFrame constructor sets up GUI and
18     // registers mouse event handlers
19     public MouseTrackerFrame()
20     {
21         super( "Demonstrating Mouse Events" );
22 
23         mousePanel = new JPanel(); // create panel
24         mousePanel.setBackground( Color.WHITE ); // set background color
25         add( mousePanel, BorderLayout.CENTER ); // add panel to JFrame
26 
27         statusBar = new JLabel( "Mouse outside JPanel" );
28         add( statusBar, BorderLayout.SOUTH ); // add label to JFrame
29 
30         // create and register listener for mouse and mouse motion events
31         MouseHandler handler = new MouseHandler();
32         mousePanel.addMouseListener( handler );
33         mousePanel.addMouseMotionListener( handler );
34     } // end MouseTrackerFrame constructor
35 
36     private class MouseHandler implements MouseListener,
37             MouseMotionListener
38     {
39         // MouseListener event handlers
40         // handle event when mouse released immediately after press
41         public void mouseClicked( MouseEvent event )
42         {
43             statusBar.setText( String.format( "Clicked at [%d, %d]",
44                 event.getX(), event.getY() ) );
45         } // end method mouseClicked
46 
47         // handle event when mouse pressed
48         public void mousePressed( MouseEvent event )
49         {
50             statusBar.setText( String.format( "Pressed at [%d, %d]",
51                 event.getX(), event.getY() ) );
52         } // end method mousePressed
53 
54         // handle event when mouse released
55         public void mouseReleased( MouseEvent event )
56         {
57             statusBar.setText( String.format( "Released at [%d, %d]",
58                 event.getX(), event.getY() ) );
59         } // end method mouseReleased

// handle event when mouse enters area
public void mouseEntered( MouseEvent event )
{
    statusBar.setText( String.format( "Mouse entered at [%d, %d]",
        event.getX(), event.getY() ) );
    mousePanel.setBackground( Color.GREEN );
} // end method mouseEntered

// handle event when mouse exits area
public void mouseExited( MouseEvent event )
{
    statusBar.setText( "Mouse outside JPanel" );
    mousePanel.setBackground( Color.WHITE );
} // end method mouseExited

// MouseMotionListener event handlers
// handle event when user drags mouse with button pressed
public void mouseDragged( MouseEvent event )
{
    statusBar.setText( String.format( "Dragged at [%d, %d]",
        event.getX(), event.getY() ) );
} // end method mouseDragged

// handle event when user moves mouse
public void mouseMoved( MouseEvent event )
{
    statusBar.setText( String.format( "Moved at [%d, %d]",
        event.getX(), event.getY() ) );
} // end method mouseMoved
} // end inner class MouseHandler
} // end class MouseTrackerFrame

## 图 14.28 | 鼠标事件处理。（第 3 部分，共 3 部分）

图 14.28 中的第 23 行创建了 JPanel mousePanel。这个 JPanel 的鼠标事件将由应用程序跟踪。第 24 行将 mousePanel 的背景颜色设置为白色。当用户将鼠标移入 mousePanel 时，应用程序会将 mousePanel 的背景颜色改为绿色。当用户将鼠标移出 mousePanel 时，应用程序将背景颜色改回白色。第 25 行将 mousePanel 添加到 JFrame。如你在第 14.5 节中所学，通常必须指定 JFrame 中 GUI 组件的布局。在该节中，我们介绍了布局管理器 FlowLayout。这里我们使用 JFrame 内容面板的默认布局——BorderLayout。这个布局管理器将组件排列到五个区域：NORTH、SOUTH、EAST、WEST 和 CENTER。NORTH 对应于容器的顶部。本示例使用 CENTER 和 SOUTH 区域。第 25 行使用 add 方法的两参数版本将 mousePanel 放置在 CENTER 区域。BorderLayout 会自动调整 CENTER 中的组件大小，使其使用 JFrame 中未被其他区域组件占用的所有空间。第 14.18.2 节更详细地讨论 BorderLayout。

构造函数中的第 27 行到第 28 行声明了 JLabel statusBar，并将其附加到 JFrame 的 SOUTH 区域。这个 JLabel 占据 JFrame 的宽度。该区域的高度由 JLabel 决定。

// Fig. 14.29: MouseTrackerFrame.java
// Testing MouseTrackerFrame.
import javax.swing.JFrame;

public class MouseTracker
{
    public static void main( String[] args )
    {
        MouseTrackerFrame mouseTrackerFrame = new MouseTrackerFrame();
        mouseTrackerFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        mouseTrackerFrame.setSize( 300, 100 ); // set frame size
        mouseTrackerFrame.setVisible( true ); // display frame
    } // end main
} // end class MouseTracker

![](img/009e962758dcc71dbc43a493362e6dc0_630_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_630_1.png)

![](img/009e962758dcc71dbc43a493362e6dc0_630_2.png)

![](img/009e962758dcc71dbc43a493362e6dc0_630_3.png)

![](img/009e962758dcc71dbc43a493362e6dc0_630_4.png)

![](img/009e962758dcc71dbc43a493362e6dc0_630_5.png)

## 图 14.29 | MouseTrackerFrame 的测试类。

第 31 行创建了内部类 MouseHandler（第 36–90 行）的一个实例 handler，它响应鼠标事件。第 32–33 行将 handler 注册为 mousePanel 鼠标事件的监听器。方法 addMouseListener 和 addMouseMotionListener 间接继承自 Component 类，分别用于注册 MouseListener 和 MouseMotionListener。MouseHandler 对象既是 MouseListener 又是 MouseMotionListener，因为该类实现了这两个接口。我们选择在这里实现两个接口，以演示一个类实现多个接口，但我们可以改为实现 MouseInputListener 接口。

当鼠标进入和退出 mousePanel 区域时，分别调用 mouseEntered（第 62–67 行）和 mouseExited（第 70–74 行）方法。mouseEntered 方法在状态栏中显示一条消息，指示鼠标进入了 JPanel，并将背景颜色改为绿色。mouseExited 方法在状态栏中显示一条消息，指示鼠标位于 JPanel 之外（参见第一个示例输出窗口），并将背景颜色改回白色。

其他五个事件在状态栏中显示一个字符串，其中包含事件以及事件发生时的坐标。MouseEvent 的 getX 和 getY 方法分别返回鼠标在事件发生时的 x 坐标和 y 坐标。

## 14.15 适配器类

许多事件监听器接口（如 MouseListener 和 MouseMotionListener）包含多个方法。在事件监听器接口中声明每个方法并不总是可取的。例如，一个应用程序可能只需要 MouseListener 中的 mouseClicked 处理器，或 MouseMotionListener 中的 mouseDragged 处理器。接口 WindowListener 指定了七个窗口事件处理方法。对于许多包含多个方法的监听器接口，包 java.awt.event 和 javax.swing.event 提供了事件监听器适配器类。适配器类实现一个接口，并为接口中的每个方法提供默认实现（方法体为空）。图 14.30 显示了几个 java.awt.event 适配器类以及它们实现的接口。你可以扩展一个适配器类来继承每个方法的默认实现，然后只覆盖你需要的用于事件处理的方法。

## 软件工程观察 14.6

当一个类实现一个接口时，该类与该接口具有 is-a 关系。该类的所有直接和间接子类都继承这个接口。因此，一个扩展了事件适配器类的类的对象就是相应事件监听器类型的对象（例如，MouseAdapter 的子类的对象就是一个 MouseListener）。

| java.awt.event 中的事件适配器类 | 实现的接口 |
|---|---|
| ComponentAdapter | ComponentListener |
| ContainerAdapter | ContainerListener |
| FocusAdapter | FocusListener |
| KeyAdapter | KeyListener |
| MouseAdapter | MouseListener |
| MouseMotionAdapter | MouseMotionListener |
| WindowAdapter | WindowListener |

图 14.30 | 事件适配器类及其在 java.awt.event 包中实现的接口。

## 扩展 MouseAdapter

图 14.31–14.32 的应用程序演示了如何确定鼠标点击的次数（即点击计数）以及如何区分不同的鼠标按钮。此应用程序中的事件监听器是内部类 MouseClickHandler（第 25–45 行）的对象，它扩展了 MouseAdapter，因此我们只需声明本例中需要的 mouseClicked 方法。

```
1  // Fig. 14.31: MouseDetailsFrame.java
2  // Demonstrating mouse clicks and distinguishing between mouse buttons.
3  import java.awt.BorderLayout;
4  import java.awt.event.MouseAdapter;
```

图 14.31 | 鼠标左键、中键和右键的点击。（第 1 部分，共 2 部分）

