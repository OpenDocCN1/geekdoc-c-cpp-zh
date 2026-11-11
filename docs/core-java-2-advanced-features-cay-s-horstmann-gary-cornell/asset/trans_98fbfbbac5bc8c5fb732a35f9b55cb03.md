
## 清单 10.7（续）

```java
11 */
12 public class PlanetTableFrame extends JFrame
13 {
14    private static final int DEFAULT_WIDTH = 600;
15    private static final int DEFAULT_HEIGHT = 500;
16
17    private static final int COLOR_COLUMN = 4;
18    private static final int IMAGE_COLUMN = 5;
19
20    private JTable table;
21    private HashSet<Integer> removedRowIndices;
22    private ArrayList<TableColumn> removedColumns;
23    private JCheckBoxMenuItem rowsItem;
24    private JCheckBoxMenuItem columnsItem;
25    private JCheckBoxMenuItem cellsItem;
26
27    private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color", "Image" };
28
29    private Object[][] cells = {
30          { "Mercury", 2440.0, 0, false, Color.YELLOW,
31             new ImageIcon(getClass().getResource("Mercury.gif")) },
32          { "Venus", 6052.0, 0, false, Color.YELLOW,
33             new ImageIcon(getClass().getResource("Venus.gif")) },
34          { "Earth", 6378.0, 1, false, Color.BLUE,
35             new ImageIcon(getClass().getResource("Earth.gif")) },
36          { "Mars", 3397.0, 2, false, Color.RED,
37             new ImageIcon(getClass().getResource("Mars.gif")) },
38          { "Jupiter", 71492.0, 16, true, Color.ORANGE,
39             new ImageIcon(getClass().getResource("Jupiter.gif")) },
40          { "Saturn", 60268.0, 18, true, Color.ORANGE,
41             new ImageIcon(getClass().getResource("Saturn.gif")) },
42          { "Uranus", 25559.0, 17, true, Color.BLUE,
43             new ImageIcon(getClass().getResource("Uranus.gif")) },
44          { "Neptune", 24766.0, 8, true, Color.BLUE,
45             new ImageIcon(getClass().getResource("Neptune.gif")) },
46          { "Pluto", 1137.0, 1, false, Color.BLACK,
47             new ImageIcon(getClass().getResource("Pluto.gif")) } };
48
49    public PlanetTableFrame()
50    {
51       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
52
53       TableModel model = new DefaultTableModel(cells, columnNames)
54          {
55             public Class<?> getColumnClass(int c)
56             {
57                return cells[0][c].getClass();
}
};
table = new JTable(model);

table.setRowHeight(100);
table.getColumnModel().getColumn(COLOR_COLUMN).setMinWidth(250);
table.getColumnModel().getColumn(IMAGE_COLUMN).setMinWidth(100);

final TableRowSorter<TableModel> sorter = new TableRowSorter<>(model);
table.setRowSorter(sorter);
sorter.setComparator(COLOR_COLUMN, Comparator.comparing(Color::getBlue)
        .thenComparing(Color::getGreen).thenComparing(Color::getRed));
sorter.setSortable(IMAGE_COLUMN, false);
add(new JScrollPane(table), BorderLayout.CENTER);

removedRowIndices = new HashSet<>();
removedColumns = new ArrayList<>();

final RowFilter<TableModel, Integer> filter = new RowFilter<TableModel, Integer>()
{
    public boolean include(Entry<? extends TableModel, ? extends Integer> entry)
    {
        return !removedRowIndices.contains(entry.getIdentifier());
    }
};

// create menu

JMenuBar menuBar = new JMenuBar();
setJMenuBar(menuBar);

JMenu selectionMenu = new JMenu("Selection");
menuBar.add(selectionMenu);

rowsItem = new JCheckBoxMenuItem("Rows");
columnsItem = new JCheckBoxMenuItem("Columns");
cellsItem = new JCheckBoxMenuItem("Cells");

rowsItem.setSelected(table.getRowSelectionAllowed());
columnsItem.setSelected(table.getColumnSelectionAllowed());
cellsItem.setSelected(table.getCellSelectionEnabled());

rowsItem.addActionListener(event ->
{
    table.clearSelection();
    table.setRowSelectionAllowed(rowsItem.isSelected());
    updateCheckboxMenuItems();
});
107  columnsItem.addActionListener(event ->
108  {
109      table.clearSelection();
110      table.setColumnSelectionAllowed(columnsItem.isSelected());
111      updateCheckboxMenuItems();
112  });
113  selectionMenu.add(columnsItem);

115  cellsItem.addActionListener(event ->
117  {
118      table.clearSelection();
119      table.setCellSelectionEnabled(cellsItem.isSelected());
120      updateCheckboxMenuItems();
121  });
122  selectionMenu.add(cellsItem);

124  JMenu tableMenu = new JMenu("Edit");
125  menuBar.add(tableMenu);

127  JMenuItem hideColumnsItem = new JMenuItem("Hide Columns");
128  hideColumnsItem.addActionListener(event ->
129  {
130      int[] selected = table.getSelectedColumns();
131      TableColumnModel columnModel = table.getColumnModel();

133      // remove columns from view, starting at the last
134      // index so that column numbers aren't affected

136      for (int i = selected.length - 1; i >= 0; i--)
137      {
138          TableColumn column = columnModel.getColumn(selected[i]);
139          table.removeColumn(column);

141          // store removed columns for "show columns" command

143          removedColumns.add(column);
144      }
145  });
146  tableMenu.add(hideColumnsItem);

148  JMenuItem showColumnsItem = new JMenuItem("Show Columns");
149  showColumnsItem.addActionListener(event ->
150  {
151      // restore all removed columns
152      for (TableColumn tc : removedColumns)
153          table.addColumn(tc);
154        removedColumns.clear();
155        });
156    tableMenu.add(showColumnsItem);
157
158    JMenuItem hideRowsItem = new JMenuItem("Hide Rows");
159    hideRowsItem.addActionListener(event ->
160    {
161        int[] selected = table.getSelectedRows();
162        for (int i : selected)
163            removedRowIndices.add(table.convertRowIndexToModel(i));
164        sorter.setRowFilter(filter);
165    });
166    tableMenu.add(hideRowsItem);
167
168    JMenuItem showRowsItem = new JMenuItem("Show Rows");
169    showRowsItem.addActionListener(event ->
170    {
171        removedRowIndices.clear();
172        sorter.setRowFilter(filter);
173    });
174    tableMenu.add(showRowsItem);
175
176    JMenuItem printSelectionItem = new JMenuItem("Print Selection");
177    printSelectionItem.addActionListener(event ->
178    {
179        int[] selected = table.getSelectedRows();
180        System.out.println("Selected rows: " + Arrays.toString(selected));
181        selected = table.getSelectedColumns();
182        System.out.println("Selected columns: " + Arrays.toString(selected));
183    });
184    tableMenu.add(printSelectionItem);
185    }
186
187    private void updateCheckboxMenuItems()
188    {
189        rowsItem.setSelected(table.getRowSelectionAllowed());
190        columnsItem.setSelected(table.getColumnSelectionAllowed());
191        cellsItem.setSelected(table.getCellSelectionEnabled());
192    }
193 }
```

- **javax.swing.table.TableModel 1.2**
  - 类 `getColumnClass(int columnIndex)` 获取此列中值的类。此信息用于排序和渲染。

| javax.swing.JTable 1.2 | 说明 |
|---|---|
| `TableColumnModel getColumnModel()` | 获取描述表格列排列的“列模型”。 |
| `void setAutoResizeMode(int mode)` | 设置表格列自动调整大小的模式。**参数：** `mode` — `AUTO_RESIZE_OFF`、`AUTO_RESIZE_NEXT_COLUMN`、`AUTO_RESIZE_SUBSEQUENT_COLUMNS`、`AUTO_RESIZE_LAST_COLUMN` 和 `AUTO_RESIZE_ALL_COLUMNS` |
| `int getRowMargin()`<br>`void setRowMargin(int margin)` | 获取或设置相邻行单元格之间的空白空间量。 |
| `int getRowHeight()`<br>`void setRowHeight(int height)` | 获取或设置表格所有行的默认高度。 |
| `int getRowHeight(int row)`<br>`void setRowHeight(int row, int height)` | 获取或设置表格给定行的高度。 |
| `ListSelectionModel getSelectionModel()` | 返回列表选择模型。你需要该模型在行、列和单元格选择之间进行选择。 |
| `boolean getRowSelectionAllowed()`<br>`void setRowSelectionAllowed(boolean b)` | 获取或设置 rowSelectionAllowed 属性。如果为 true，则当用户单击单元格时选择行。 |
| `boolean getColumnSelectionAllowed()`<br>`void setColumnSelectionAllowed(boolean b)` | 获取或设置 columnSelectionAllowed 属性。如果为 true，则当用户单击单元格时选择列。 |
| `boolean getCellSelectionEnabled()` | 如果 rowSelectionAllowed 和 columnSelectionAllowed 均为 true，则返回 true。 |
| `void setCellSelectionEnabled(boolean b)` | 将 rowSelectionAllowed 和 columnSelectionAllowed 都设置为 b。 |
| `void addColumn(TableColumn column)` | 将一列添加为表格视图的最后一列。 |
