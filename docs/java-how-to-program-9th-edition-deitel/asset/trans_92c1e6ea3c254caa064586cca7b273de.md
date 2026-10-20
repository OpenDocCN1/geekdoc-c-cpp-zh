
SINGLE_INTERVAL_SELECTION 列表。当您执行应用程序时，尝试使用前面描述的选择技术来在两个列表中选择项目。

// Fig. 14.25: MultipleSelectionFrame.java
// Copying items from one List to another.
import java.awt.FlowLayout;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.JFrame;
import javax.swing.JList;
import javax.swing.JButton;
import javax.swing.JScrollPane;
import javax.swing.ListSelectionModel;

public class MultipleSelectionFrame extends JFrame
{
    private JList colorJList; // list to hold color names
    private JList copyJList; // list to copy color names into
    private JButton copyJButton; // button to copy selected names
    private static final String[] colorNames = { "Black", "Blue", "Cyan", "Dark Gray", "Gray", "Green", "Light Gray", "Magenta", "Orange", "Pink", "Red", "White", "Yellow" };

    // MultipleSelectionFrame constructor
    public MultipleSelectionFrame()
    {
        super( "Multiple Selection Lists" );
        setLayout( new FlowLayout() ); // set frame layout

        colorJList = new JList( colorNames ); // holds names of all colors
        colorJList.setVisibleRowCount( 5 ); // show five rows
        colorJList.setSelectionMode(
            ListSelectionModel.MULTIPLE_INTERVAL_SELECTION );
        add( new JScrollPane( colorJList ) ); // add list with scrollpane

        copyJButton = new JButton( "Copy >>>" ); // create copy button
        copyJButton.addActionListener(

            new ActionListener() // anonymous inner class
            {
                // handle button event
                public void actionPerformed( ActionEvent event )
                {
                    // place selected values in copyJList
                    copyJList.setListData( colorJList.getSelectedValues() );
                } // end method actionPerformed
            } // end anonymous inner class
        ); // end call to addActionListener

        add( copyJButton ); // add copy button to JFrame

        copyJList = new JList(); // create list to hold copied color names
        copyJList.setVisibleRowCount( 5 ); // show 5 rows
        copyJList.setFixedCellWidth( 100 ); // set width
        copyJList.setFixedCellHeight( 15 ); // set height
        copyJList.setSelectionMode(
            ListSelectionModel.SINGLE_INTERVAL_SELECTION );
        add( new JScrollPane( copyJList ) ); // add list with scrollpane
    } // end MultipleSelectionFrame constructor
} // end class MultipleSelectionFrame

图14.25 | 允许多项选择的JList。（第2部分，共2部分。）

```
// Fig. 14.26: MultipleSelectionTest.java
// Testing MultipleSelectionFrame.
import javax.swing.JFrame;

public class MultipleSelectionTest
{
    public static void main( String[] args )
    {
        MultipleSelectionFrame multipleSelectionFrame =
           new MultipleSelectionFrame();
        multipleSelectionFrame.setDefaultCloseOperation(
            JFrame.EXIT_ON_CLOSE );
        multipleSelectionFrame.setSize( 350, 150 ); // set frame size
        multipleSelectionFrame.setVisible( true ); // display frame
    } // end main
} // end class MultipleSelectionTest
```

![](img/009e962758dcc71dbc43a493362e6dc0_625_0.png)

图14.26 | MultipleSelectionFrame的测试类。

图14.25的第27行创建JList colorJList，并使用数组colorNames中的字符串对其进行初始化。第28行将colorJList中的可见行数设置为5。第29–30行指定colorJList是一个MULTIPLE_INTERVAL_SELECTION列表。第31行向JFrame添加一个包含colorJList的新JScrollPane。第49–55行为copyJList执行类似任务，该列表被声明为SINGLE_INTERVAL_SELECTION列表。如果JList不包含项目，它将不会显示在FlowLayout中。因此，第51–52行使用JList方法setFixedCellWidth和setFixedCellHeight将copyJList的宽度设置为100像素，并将JList中每个项目的高度设置为15像素。

通常，由另一个GUI组件生成的事件（称为外部事件）指定何时应处理JList中的多个选择。在此示例中，用户单击名为copyJButton的JButton，以触发将colorJList中选定的项目复制到copyJList的事件。

第34–45行为copyJButton声明、创建并注册一个ActionListener。当用户单击copyJButton时，方法actionPerformed（第39–43行）使用JList方法setListData来设置copyJList中显示的项目。第42行调用colorJList的getSelectedValues方法，该方法返回一个Object数组，表示colorJList中选定的项目。在此示例中，返回的数组作为参数传递给copyJList的setListData方法。

您可能想知道为什么第42行可以使用copyJList，尽管应用程序直到第49行才创建它引用的对象。请记住，方法actionPerformed（第39–43行）直到用户按下copyJButton后才执行，而按下按钮必须等到构造函数完成执行且应用程序显示GUI之后才能发生。在应用程序执行到此时，copyJList已经用一个新的JList对象初始化了。

## 14.14 鼠标事件处理

本节介绍用于处理鼠标事件的MouseListener和MouseMotionListener事件监听器接口。鼠标事件可以由任何派生自java.awt.Component的GUI组件处理。MouseListener和MouseMotionListener接口的方法总结在图14.27中。包javax.swing.event包含接口MouseInputListener，该接口扩展了MouseListener和MouseMotionListener，以创建一个包含所有MouseListener和MouseMotionListener方法的单一接口。如果为某个Component注册了相应的事件监听器对象，则当鼠标与该Component交互时，将调用MouseListener和MouseMotionListener方法。

每个鼠标事件处理方法都接收一个MouseEvent对象作为参数，该对象包含有关所发生鼠标事件的信息，包括其位置的x和y坐标。这些坐标是从事件发生的GUI组件的左上角开始测量的。x坐标从0开始，从左到右递增。y坐标从0开始，从上到下递增。类InputEvent（MouseEvent的超类）的方法和常量使您能够确定用户单击了哪个鼠标按钮。

MouseListener和MouseMotionListener接口方法

MouseListener接口的方法

```
public void mousePressed( MouseEvent event )
```

当鼠标光标位于某个组件上且按下鼠标按钮时调用。

```
public void mouseClicked( MouseEvent event )
```

当鼠标光标停留在某个组件上且按下并释放鼠标按钮时调用。此事件之前总是会调用mousePressed。

```
public void mouseReleased( MouseEvent event )
```

当按下鼠标按钮后释放该按钮时调用。此事件之前总是会调用mousePressed以及一次或多次mouseDragged。

图14.27 | MouseListener和MouseMotionListener接口方法。（第1部分，共2部分。）

## MouseListener和MouseMotionListener接口方法

```
public void mouseEntered( MouseEvent event )
```

当鼠标光标进入某个组件的边界时调用。

```
public void mouseExited( MouseEvent event )
```

当鼠标光标离开某个组件的边界时调用。

MouseMotionListener接口的方法

```
public void mouseDragged( MouseEvent event )
```

当鼠标光标位于某个组件上，按下鼠标按钮并移动鼠标（同时保持按钮按下）时调用。此事件之前总是会调用mousePressed。所有拖动事件都发送到用户开始拖动鼠标时所在的组件。

```
public void mouseMoved( MouseEvent event )
```

当鼠标光标位于某个组件上并移动鼠标（不按下任何鼠标按钮）时调用。所有移动事件都发送到鼠标当前所在的组件。

图14.27 | MouseListener和MouseMotionListener接口方法。（第2部分，共2部分。）

## 软件工程观察 14.5

对mouseDragged的调用被发送到拖动开始所在组件的MouseMotionListener。类似地，拖动操作结束时的mouseReleased调用被发送到拖动操作开始所在组件的MouseListener。

Java还提供了MouseWheelListener接口，使应用程序能够响应鼠标滚轮的旋转。该接口声明了方法mouseWheelMoved，该方法接收MouseWheelEvent作为其参数。MouseWheelEvent类（MouseEvent的子类）包含使事件处理程序能够获取有关滚轮旋转量的信息的方法。

## 在JPanel上跟踪鼠标事件

MouseTracker应用程序（图14.28–14.29）演示了MouseListener和MouseMotionListener接口方法。事件处理程序类（第36–90行）实现了这两个接口。当您的类同时实现这两个接口时，您必须声明这两个接口中的所有七个方法。此示例中的每个鼠标事件都会在附加到窗口底部的名为statusBar的JLabel中显示一个字符串。

```
// Fig. 14.28: MouseTrackerFrame.java
// Demonstrating mouse events.
import java.awt.Color;
import java.awt.BorderLayout;
import java.awt.event.MouseListener;
import java.awt.event.MouseMotionListener;
import java.awt.event.MouseEvent;
```

图14.28 | 鼠标事件处理。（第1部分，共3部分。）

