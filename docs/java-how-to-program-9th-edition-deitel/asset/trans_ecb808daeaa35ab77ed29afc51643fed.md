

![](img/009e962758dcc71dbc43a493362e6dc0_645_0.png)

图 14.40 | FlowLayoutFrame 的测试类。 （第 2 部分，共 2 部分。）

每个按钮的事件处理程序都由单独的匿名内部类对象指定（图 14.39，第 30–43 行、第 48–61 行和第 66–79 行），并且在每种情况下，方法 actionPerformed 都执行两个语句。例如，左按钮 leftJButton 的事件处理程序中的第 37 行使用 FlowLayout 方法 setAlignment 将 FlowLayout 的对齐方式更改为左对齐（FlowLayout.LEFT）的 FlowLayout。第 40 行使用 LayoutManager 接口方法 layoutContainer（由所有布局管理器继承）来指定 JFrame 应根据调整后的布局重新排列。根据单击了哪个按钮，每个按钮的 actionPerformed 方法将 FlowLayout 的对齐方式设置为 FlowLayout.LEFT（第 37 行）、FlowLayout.CENTER（第 55 行）或 FlowLayout.RIGHT（第 73 行）。

### 14.18.2 BorderLayout

BorderLayout 布局管理器（JFrame 的默认布局管理器）将组件排列到五个区域：NORTH、SOUTH、EAST、WEST 和 CENTER。NORTH 对应于容器的顶部。类 BorderLayout 扩展 Object 并实现接口 LayoutManager2（LayoutManager 的子接口，增加了用于增强布局处理的几个方法）。

BorderLayout 将容器限制为最多包含五个组件——每个区域一个。放置在每个区域中的组件可以是附加其他组件的容器。放置在 NORTH 和 SOUTH 区域中的组件水平延伸到容器的两侧，并且与放置在这些区域中的组件一样高。EAST 和 WEST 区域在 NORTH 和 SOUTH 区域之间垂直扩展，并且与放置在这些区域中的组件一样宽。放置在 CENTER 区域中的组件扩展以填充布局中所有剩余空间（这是图 14.37 中的 JTextArea 占据整个窗口的原因）。如果五个区域都已占用，则整个容器的空间将被 GUI 组件覆盖。如果 NORTH 或 SOUTH 区域未被占用，则 EAST、CENTER 和 WEST 区域中的 GUI 组件将垂直扩展以填充剩余空间。如果 EAST 或 WEST 区域未被占用，则 CENTER 区域中的 GUI 组件将水平扩展以填充剩余空间。如果 CENTER 区域未被占用，则该区域将保持为空——其他 GUI 组件不会扩展以填充剩余空间。图 14.41–14.42 的应用程序通过使用五个 JButtons 来演示 BorderLayout 布局管理器。

```
// Fig. 14.41: BorderLayoutFrame.java
// Demonstrating BorderLayout.
import java.awt.BorderLayout;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.JFrame;
import javax.swing.JButton;

public class BorderLayoutFrame extends JFrame implements ActionListener
{
    private JButton[] buttons; // array of buttons to hide portions
    private static final String[] names = { "Hide North", "Hide South", "Hide East", "Hide West", "Hide Center" };
    private BorderLayout layout; // BorderLayout object

    // set up GUI and event handling
    public BorderLayoutFrame()
    {
        super( "BorderLayout Demo" );

        layout = new BorderLayout( 5, 5 ); // 5 pixel gaps
        setLayout( layout ); // set frame layout
        buttons = new JButton[ names.length ]; // set size of array

        // create JButtons and register listeners for them
        for ( int count = 0; count < names.length; count++ )
        {
            buttons[ count ] = new JButton( names[ count ] );
            buttons[ count ].addActionListener( this );
        } // end for

        add( buttons[ 0 ], BorderLayout.NORTH ); // add button to north
        add( buttons[ 1 ], BorderLayout.SOUTH ); // add button to south
        add( buttons[ 2 ], BorderLayout.EAST ); // add button to east
        add( buttons[ 3 ], BorderLayout.WEST ); // add button to west
        add( buttons[ 4 ], BorderLayout.CENTER ); // add button to center
    } // end BorderLayoutFrame constructor

    // handle button events
    public void actionPerformed( ActionEvent event )
    {
        // check event source and lay out content pane correspondingly
        for ( JButton button : buttons )
        {
            if ( event.getSource() == button )
                button.setVisible( false ); // hide button clicked
            else
                button.setVisible( true ); // show other buttons
        } // end for

        layout.layoutContainer( getContentPane() ); // lay out content pane
    } // end method actionPerformed
} // end class BorderLayoutFrame
```

图 14.41 | 包含五个按钮的 BorderLayout。 （第 2 部分，共 2 部分。）

```
// Fig. 14.42: BorderLayoutDemo.java
// Testing BorderLayoutFrame.
import javax.swing.JFrame;

public class BorderLayoutDemo
{
    public static void main( String[] args )
    {
        BorderLayoutFrame borderLayoutFrame = new BorderLayoutFrame();
        borderLayoutFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        borderLayoutFrame.setSize( 300, 200 ); // set frame size
        borderLayoutFrame.setVisible( true ); // display frame
    } // end main
} // end class BorderLayoutDemo
```

![](img/009e962758dcc71dbc43a493362e6dc0_647_0.png)

图 14.42 | BorderLayoutFrame 的测试类。

图 14.41 的第 21 行创建了一个 BorderLayout。构造函数参数分别指定水平排列的组件之间的像素数（水平间隙空间）和垂直排列的组件之间的像素数（垂直间隙空间）。默认情况下，水平和垂直间隙空间均为一个像素。第 22 行使用方法 setLayout 将 content pane 的布局设置为 layout。

我们使用 Container 方法 add 的另一个版本将组件添加到 BorderLayout，该版本接受两个参数——要添加的组件以及组件应出现的区域。例如，第 32 行指定 buttons[ 0 ] 应出现在 NORTH 区域。组件可以按任何顺序添加，但每个区域只能添加一个组件。

**外观与感觉观察 14.18**

> 如果在将组件添加到 BorderLayout 时未指定区域，布局管理器会假定组件应添加到区域 BorderLayout.CENTER。

**常见编程错误 14.6**

> 当向 BorderLayout 中的一个区域添加多个组件时，只有最后添加到该区域的组件才会被显示。没有错误指示此问题。

在本示例中，类 BorderLayoutFrame 直接实现 ActionListener，因此 BorderLayoutFrame 将处理 JButtons 的事件。因此，第 29 行将 this 引用传递给每个 JButton 的 addActionListener 方法。当用户单击布局中的特定 JButton 时，方法 actionPerformed（第 40–52 行）执行。增强的 for 语句在第 43–49 行使用 if...else 隐藏生成事件的特定 JButton。方法 setVisible（从类 Component 继承到 JButton）被调用并带有 false 参数（第 46 行）以隐藏 JButton。如果数组中的当前 JButton 不是生成事件的按钮，则方法 setVisible 被调用并带有 true 参数（第 48 行）以确保 JButton 显示在屏幕上。第 51 行使用 LayoutManager 方法 layoutContainer 重新计算 content pane 的布局。请注意，在图 14.42 的屏幕截图中，随着在其他区域隐藏和显示 JButtons，BorderLayout 中的某些区域形状会发生变化。尝试调整应用程序窗口的大小，以查看各个区域如何根据窗口的宽度和高度调整大小。对于更复杂的布局，将组件分组到 JPanels 中，每个面板使用单独的布局管理器。使用默认的 BorderLayout 或其他布局将 JPanels 放置在 JFrame 上。

### 14.18.3 GridLayout

GridLayout 布局管理器将容器划分为网格，以便组件可以放置在行和列中。类 GridLayout 直接继承自类 Object 并实现接口 LayoutManager。GridLayout 中的每个组件具有相同的宽度和高度。组件从网格的左上角单元格开始添加到 GridLayout，并按从左到右的顺序进行，直到该行填满。然后该过程在网格的下一行从左到右继续，依此类推。图 14.43–14.44 的应用程序通过使用六个 JButtons 来演示 GridLayout 布局管理器。

第 24–25 行创建了两个 GridLayout 对象。第 24 行使用的 GridLayout 构造函数指定了一个具有 2 行、3 列、组件之间 5 像素的水平间隙空间以及组件之间 5 像素的垂直间隙空间的 GridLayout。

