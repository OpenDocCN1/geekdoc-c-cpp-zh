
```java
13 public class TableTest
14 {
15     public static void main(String[] args)
16     {
17         EventQueue.invokeLater(() ->
18             {
19                 var frame = new PlanetTableFrame();
20                 frame.setTitle("TableTest");
21                 frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
22                 frame.setVisible(true);
23             });
24     }
25 }
26
27 /**
28  * This frame contains a table of planet data.
29  */
30 class PlanetTableFrame extends JFrame
31 {
32     private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color" };
33     private Object[][] cells =
34         {
35             { "Mercury", 2440.0, 0, false, Color.YELLOW },
36             { "Venus", 6052.0, 0, false, Color.YELLOW },
37             { "Earth", 6378.0, 1, false, Color.BLUE },
38             { "Mars", 3397.0, 2, false, Color.RED },
39             { "Jupiter", 71492.0, 16, true, Color.ORANGE },
40             { "Saturn", 60268.0, 18, true, Color.ORANGE },
41             { "Uranus", 25559.0, 17, true, Color.BLUE },
42             { "Neptune", 24766.0, 8, true, Color.BLUE },
43             { "Pluto", 1137.0, 1, false, Color.BLACK }
44         };
45
46     public PlanetTableFrame()
47     {
48         var table = new JTable(cells, columnNames);
49         table.setAutoCreateRowSorter(true);
50         add(new JScrollPane(table), BorderLayout.CENTER);
51         var printButton = new JButton("Print");
52         printButton.addActionListener(event ->
53             {
54                 try { table.print(); }
55                 catch (SecurityException | PrinterException ex) { ex.printStackTrace(); }
56             });
57         var buttonPanel = new JPanel();
58         buttonPanel.add(printButton);
59         add(buttonPanel, BorderLayout.SOUTH);
60         pack();
61     }
62 }
```

| `javax.swing.JTable` | `1.2` |
| --- | --- |
| `JTable(Object[][] entries, Object[] columnNames)` | 用默认表模型构造一个表。 |
| `void print()` `5.0` | 显示打印对话框并打印该表。 |
| `boolean getAutoCreateRowSorter()` `6` |  |
| `void setAutoCreateRowSorter(boolean newValue)` `6` | 获取或设置 autoCreateRowSorter 属性。默认值为 false。设置后，每当模型发生变化时，都会自动设置一个默认行排序器。 |
| `boolean getFillsViewportHeight()` `6` |  |
| `void setFillsViewportHeight(boolean newValue)` `6` | 获取或设置 fillsViewportHeight 属性。默认值为 false。设置后，表始终填满其所在的视口。 |

## 11.1.2 表模型

在前面的示例中，表数据存储在一个二维数组中。不过，在你自己的代码中通常不应采用这种策略。与其将数据倾倒进数组再以表的形式显示，不如考虑实现你自己的表模型。

表模型实现起来特别简单，因为你可以利用实现了大多数所需方法的 AbstractTableModel 类。你只需要提供三个方法：

```java
public int getRowCount();
public int getColumnCount();
public Object getValueAt(int row, int column);
```

实现 getValueAt 方法有很多方式。例如，如果你想显示一个包含数据库查询结果的 RowSet 的内容，只需提供这个方法：

```java
public Object getValueAt(int r, int c)
{
    try
    {
        rowSet.absolute(r + 1);
        return rowSet.getObject(c + 1);
    }
    catch (SQLException e)
    {
        e.printStackTrace();
        return null;
    }
}
```

我们的示例程序甚至更简单。我们构造一个表来显示一些计算得到的值——即投资在不同利率情景下的增长（见图 11.4）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_641_0.png)

**图 11.4** 投资的增长

`getValueAt` 方法计算相应的值并对其进行格式化：

```java
public Object getValueAt(int r, int c)
{
    double rate = (c + minRate) / 100.0;
    int periods = r;
    double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, periods);
    return String.format("%.2f", futureBalance);
}
```

`getRowCount` 和 `getColumnCount` 方法只是返回行数和列数：

```java
public int getRowCount() { return years; }
public int getColumnCount() { return maxRate - minRate + 1; }
```

如果你不提供列名，`AbstractTableModel` 的 `getColumnName` 方法会将列命名为 A、B、C 等。要更改默认列名，请重写 `getColumnName` 方法。在这个例子中，我们只是用利率来标记每一列。

```java
public String getColumnName(int c) { return (c + minRate) + "%"; }
```

你可以在程序清单 11.2 中找到完整的源代码。

**程序清单 11.2** `tableModel/InvestmentTable.java`

```java
1  package tableModel;
2
3  import java.awt.*;
4
5  import javax.swing.*;
6  import javax.swing.table.*;
7
8  /**
9   * This program shows how to build a table from a table model.
10  * @version 1.04 2018-05-01
11  * @author Cay Horstmann
12  */
13 public class InvestmentTable
14 {
15    public static void main(String[] args)
16    {
17       EventQueue.invokeLater(() ->
18          {
19             var frame = new InvestmentTableFrame();
20             frame.setTitle("InvestmentTable");
21             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
22             frame.setVisible(true);
23          });
24    }
25 }
26
27 /**
28  * This frame contains the investment table.
29  */
30 class InvestmentTableFrame extends JFrame
31 {
32    public InvestmentTableFrame()
33    {
34       var model = new InvestmentTableModel(30, 5, 10);
35       var table = new JTable(model);
36       add(new JScrollPane(table));
37       pack();
38    }
39 }
40
41 /**
42  * This table model computes the cell entries each time they are requested. The table contents
43  * shows the growth of an investment for a number of years under different interest rates.
44  */
45 class InvestmentTableModel extends AbstractTableModel
46 {
47    private static double INITIAL_BALANCE = 100000.0;
48
49    private int years;
50    private int minRate;
51    private int maxRate;
52
53    /**
54     * Constructs an investment table model.
55     * @param y the number of years
56     * @param r1 the lowest interest rate to tabulate
57     * @param r2 the highest interest rate to tabulate
58     */
59    public InvestmentTableModel(int y, int r1, int r2)
60    {
61       years = y;
62       minRate = r1;
63       maxRate = r2;
64    }
65
66    public int getRowCount()
67    {
68       return years;
69    }
70
71    public int getColumnCount()
72    {
73       return maxRate - minRate + 1;
74    }
75
76    public Object getValueAt(int r, int c)
77    {
78       double rate = (c + minRate) / 100.0;
79       int nperiods = r;
80       double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, nperiods);
81       return String.format("%.2f", futureBalance);
82    }
83
84    public String getColumnName(int c)
85    {
86       return (c + minRate) + "%";
87    }
88 }
```

| `javax.swing.table.TableModel` | `1.2` |
| --- | --- |
| `int getRowCount()`<br>`int getColumnCount()` | 获取表模型中的行数和列数。 |
| `Object getValueAt(int row, int column)` | 获取给定行和列处的值。 |
| `void setValueAt(Object newValue, int row, int column)` | 在给定行和列处设置新值。 |
| `boolean isCellEditable(int row, int column)` | 如果给定行和列处的单元格可编辑，则返回 true。 |
| `String getColumnName(int column)` | 获取列标题。 |

## 11.1.3 处理行和列

在本小节中，你将看到如何操作表中的行和列。阅读这些内容时，请记住 Swing 表是相当不对称的——你可以对行和列执行的操作是不同的。表组件经过优化，用于显示结构相同的信息行，例如数据库查询的结果，而不是任意的二维对象网格。你将在整个小节中看到这种不对称性。

### 11.1.3.1 列类

在下一个示例中，我们再次显示行星数据，但这一次我们想向表提供更多关于列类型的信息。这是通过定义表模型的 `Class<?> getColumnClass(int columnIndex)` 方法返回描述列类型的类来实现的。

JTable 类使用此信息为该类选择合适的渲染器。表 11.1 显示了默认的渲染操作。

你可以在图 11.5 中看到复选框和图像。（感谢 Jim Evins 提供行星图像！）

要渲染其他类型，你可以安装自定义渲染器——参见第 639 页的 11.1.4 节“单元格渲染与编辑”。
