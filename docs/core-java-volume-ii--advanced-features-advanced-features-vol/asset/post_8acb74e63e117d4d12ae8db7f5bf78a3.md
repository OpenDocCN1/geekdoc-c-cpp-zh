
```java
table.addColumn(new TableColumn(modelColumnIndex));
```

You can have multiple table columns that view the same column of the model.

The program in Listing 11.3 demonstrates selection and filtering of rows and columns.

## Listing 11.3 `tableRowColumn/PlanetTableFrame.java`

```java
package tableRowColumn;

import java.awt.*;
import java.util.*;

import javax.swing.*;
import javax.swing.table.*;

/**
 * This frame contains a table of planet data.
 */
public class PlanetTableFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 600;
    private static final int DEFAULT_HEIGHT = 500;

    public static final int COLOR_COLUMN = 4;
    public static final int IMAGE_COLUMN = 5;

    private JTable table;
    private HashSet<Integer> removedRowIndices;
    private ArrayList<TableColumn> removedColumns;
    private JCheckBoxMenuItem rowsItem;
    private JCheckBoxMenuItem columnsItem;
    private JCheckBoxMenuItem cellsItem;

    private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color", "Image" };

    private Object[][] cells =
    {
        { "Mercury", 2440.0, 0, false, Color.YELLOW,
            new ImageIcon(getClass().getResource("Mercury.gif")) },
        { "Venus", 6052.0, 0, false, Color.YELLOW,
            new ImageIcon(getClass().getResource("Venus.gif")) },
        { "Earth", 6378.0, 1, false, Color.BLUE,
            new ImageIcon(getClass().getResource("Earth.gif")) },
        { "Mars", 3397.0, 2, false, Color.RED,
            new ImageIcon(getClass().getResource("Mars.gif")) },
        { "Jupiter", 71492.0, 16, true, Color.ORANGE,
            new ImageIcon(getClass().getResource("Jupiter.gif")) },
        { "Saturn", 60268.0, 18, true, Color.ORANGE,
            new ImageIcon(getClass().getResource("Saturn.gif")) },
        { "Uranus", 25559.0, 17, true, Color.BLUE,
            new ImageIcon(getClass().getResource("Uranus.gif")) },
        { "Neptune", 24760.0, 8, true, Color.BLUE,
            new ImageIcon(getClass().getResource("Neptune.gif")) },
        { "Pluto", 1137.0, 1, false, Color.BLACK,
            new ImageIcon(getClass().getResource("Pluto.gif")) }
    };

    public PlanetTableFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        var model = new DefaultTableModel(cells, columnNames)
        {
            public Class<?> getColumnClass(int c)
            {
                return cells[0][c].getClass();
            }
        };

        table = new JTable(model);

        table.setRowHeight(100);

        table.getColumnModel().getColumn(COLOR_COLUMN).setMinWidth(250);
        table.getColumnModel().getColumn(IMAGE_COLUMN).setMinWidth(100);

        var sorter = new TableRowSorter<TableModel>(model);
        table.setRowSorter(sorter);
        sorter.setComparator(COLOR_COLUMN, Comparator.comparing(Color::getBlue)
            .thenComparing(Color::getGreen).thenComparing(Color::getRed));
        sorter.setSortable(IMAGE_COLUMN, false);
        add(new JScrollPane(table), BorderLayout.CENTER);

        removedRowIndices = new HashSet<>();
        removedColumns = new ArrayList<>();

        var filter = new RowFilter<TableModel, Integer>()
        {
            public boolean include(Entry<? extends TableModel, ? extends Integer> entry)
            {
                return !removedRowIndices.contains(entry.getIdentifier());
            }
        };

        // create menu

        var menuBar = new JMenuBar();
        setJMenuBar(menuBar);

        var selectionMenu = new JMenu("Selection");
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
        selectionMenu.add(rowsItem);

        columnsItem.addActionListener(event ->
        {
            table.clearSelection();
            table.setColumnSelectionAllowed(columnsItem.isSelected());
            updateCheckboxMenuItems();
        });
        selectionMenu.add(columnsItem);

        cellsItem.addActionListener(event ->
        {
            table.clearSelection();
            table.setCellSelectionEnabled(cellsItem.isSelected());
            updateCheckboxMenuItems();
        });
        selectionMenu.add(cellsItem);

        var tableMenu = new JMenu("Edit");
        menuBar.add(tableMenu);

        var hideColumnsItem = new JMenuItem("Hide Columns");
        hideColumnsItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedColumns();
            TableColumnModel columnModel = table.getColumnModel();

            // remove columns from view, starting at the last
            // index so that column numbers aren't affected

            for (int i = selected.length - 1; i >= 0; i--)
            {
                TableColumn column = columnModel.getColumn(selected[i]);
                table.removeColumn(column);

                // store removed columns for "show columns" command

                removedColumns.add(column);
            }
        });
        tableMenu.add(hideColumnsItem);

        var showColumnsItem = new JMenuItem("Show Columns");
        showColumnsItem.addActionListener(event ->
        {
            // restore all removed columns
            for (TableColumn tc : removedColumns)
                table.addColumn(tc);
            removedColumns.clear();
        });
        tableMenu.add(showColumnsItem);

        var hideRowsItem = new JMenuItem("Hide Rows");
        hideRowsItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedRows();
            for (int i : selected)
                removedRowIndices.add(table.convertRowIndexToModel(i));
            sorter.setRowFilter(filter);
        });
        tableMenu.add(hideRowsItem);

        var showRowsItem = new JMenuItem("Show Rows");
        showRowsItem.addActionListener(event ->
        {
            removedRowIndices.clear();
            sorter.setRowFilter(filter);
        });
        tableMenu.add(showRowsItem);

        var printSelectionItem = new JMenuItem("Print Selection");
        printSelectionItem.addActionListener(event ->
        {
            int[] selected = table.getSelectedRows();
            System.out.println("Selected rows: " + Arrays.toString(selected));
            selected = table.getSelectedColumns();
            System.out.println("Selected columns: " + Arrays.toString(selected));
        });
        tableMenu.add(printSelectionItem);
    }

    private void updateCheckboxMenuItems()
    {
        rowsItem.setSelected(table.getRowSelectionAllowed());
        columnsItem.setSelected(table.getColumnSelectionAllowed());
        cellsItem.setSelected(table.getCellSelectionEnabled());
    }
}
```

| **javax.swing.table.TableModel 1.2** |
| --- |
| • `Class getColumnClass(int columnIndex)`<br>gets the class for the values in this column. This information is used for sorting and rendering. |

| **javax.swing.JTable 1.2** |
| --- |
| • `TableColumnModel getColumnModel()`<br>gets the column model that describes the arrangement of the table columns.<br><br>• `void setAutoResizeMode(int mode)`<br>sets the mode for automatic resizing of table columns.<br>*Parameters:* mode&nbsp;&nbsp;One of AUTO_RESIZE_OFF, AUTO_RESIZE_NEXT_COLUMN, AUTO_RESIZE_SUBSEQUENT_COLUMNS, AUTO_RESIZE_LAST_COLUMN, and AUTO_RESIZE_ALL_COLUMNS<br><br>• `int getRowMargin()`<br><br>• `void setRowMargin(int margin)`<br>gets or sets the amount of empty space between cells in adjacent rows.<br><br>• `int getRowHeight()`<br><br>• `void setRowHeight(int height)`<br>gets or sets the default height of all rows of the table.<br><br>• `int getRowHeight(int row)`<br><br>• `void setRowHeight(int row, int height)`<br>gets or sets the height of the given row of the table. |

| **javax.swing.table.TableColumn 1.2** |
| --- |
| • `TableColumn(int modelColumnIndex)`<br>constructs a table column for viewing the model column with the given index.<br>• `void setPreferredWidth(int width)`<br>• `void setMinWidth(int width)`<br>• `void setMaxWidth(int width)`<br>sets the preferred, minimum, and maximum width of this table column to width.<br>• `void setWidth(int width)`<br>sets the actual width of this column to width.<br>• `void setResizable(boolean b)`<br>If b is true, this column is resizable. |

| **javax.swing.ListSelectionModel 1.2** |
| --- |
| • `void setSelectionMode(int mode)`<br>*Parameters:* mode One of SINGLE_SELECTION, SINGLE_INTERVAL_SELECTION, and MULTIPLE_INTERVAL_SELECTION |

| **`javax.swing.DefaultRowSorter<R, I>` 6** |
| --- |
| • `void setComparator(int column, Comparator<?> comparator)`<br>sets the comparator to be used with the given column.<br>• `void setSortable(int column, boolean enabled)`<br>enables or disables sorting for the given column.<br>• `void setRowFilter(RowFilter<? super M, ? super I> filter)`<br>sets the row filter. |

| **`javax.swing.table.TableRowSorter<R extends TableModel>` 6** |
| --- |
| • `void setStringConverter(TableStringConverter stringConverter)`<br>sets the string converter used for sorting and filtering. |

| **javax.swing.table.TableStringConverter 6** |
| --- |
| • `abstract String toString(TableModel model, int row, int column)`<br>converts the model value at the given location to a string; you can override this method. |
