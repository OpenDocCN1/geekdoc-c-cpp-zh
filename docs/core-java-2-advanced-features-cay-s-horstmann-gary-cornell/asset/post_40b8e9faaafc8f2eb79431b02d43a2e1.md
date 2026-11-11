
## javax.swing.JTable 1.2 (Continued)

- `void moveColumn(int from, int to)`  
  moves the column whose table index is `from` so that its index becomes `to`. Only the view is affected.
- `void removeColumn(TableColumn column)`  
  removes the given column from the view.
- `int convertRowIndexToModel(int index)`
- `int convertColumnIndexToModel(int index)`  
  returns the model index of the row or column with the given index. This value is different from index when rows are sorted or filtered, or when columns are moved or removed.
- `void setRowSorter(RowSorter<? extends TableModel> sorter)`  
  sets the row sorter.

## javax.swing.table.TableColumnModel 1.2

- `TableColumn getColumn(int index)`  
  gets the table column object that describes the column with the given view index.

## javax.swing.table.TableColumn 1.2

- `TableColumn(int modelColumnIndex)`  
  constructs a table column for viewing the model column with the given index.
- `void setPreferredWidth(int width)`
- `void setMinWidth(int width)`
- `void setMaxWidth(int width)`  
  sets the preferred, minimum, and maximum width of this table column to `width`.
- `void setWidth(int width)`  
  sets the actual width of this column to `width`.
- `void setResizable(boolean b)`  
  If `b` is true, the column is resizable.

## javax.swing.RowFilter<M, I> 1.6 (Continued)

- `static <M,I> RowFilter<M,I> numberFilter(RowFilter.ComparisonType type, Number number, int... indices)`  
  returns a filter that includes rows containing values that match the given comparison to the given number or date. The comparison type is one of EQUAL, NOT_EQUAL, AFTER, or BEFORE. If any column model indexes are given, only those columns are searched; otherwise, all columns are searched. For the number filter, the class of the cell value must match the class of number.
- `static <M,I> RowFilter<M,I> dateFilter(RowFilter.ComparisonType type, Date date, int... indices)`  
  returns a filter that includes rows containing values that match the given comparison to the given number or date. The comparison type is one of EQUAL, NOT_EQUAL, AFTER, or BEFORE. If any column model indexes are given, only those columns are searched; otherwise, all columns are searched. For the date filter, the class of the cell value must match the class of date.
- `static <M,I> RowFilter<M,I> regexFilter(String regex, int... indices)`  
  returns a filter that includes rows that have a string value matching the given regular expression. If any column model indexes are given, only those columns are searched; otherwise, all columns are searched. Note that the string returned by the getStringValue method of RowFilter.Entry is matched.
- `static <M,I> RowFilter<M,I> andFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`
- `static <M,I> RowFilter<M,I> orFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`  
  returns a filter that includes the entries included by all filters or at least one of the filters.
- `static <M,I> RowFilter<M,I> notFilter(RowFilter<M,I> filter)`  
  returns a filter that includes the entries not included by the given filter.

## javax.swing.RowFilter.Entry<M, I> 1.6

- `I getIdentifier()`  
  returns the identifier of this row entry.
- `M getModel()`  
  returns the model of this row entry.
- `Object getValue(int index)`  
  returns the value stored at the given index of this row.
- `int getValueCount()`  
  returns the number of values stored in this row.
- `String getStringValue()`  
  returns the value stored at the given index of this row, converted to a string. The TableRowSorter produces entries whose getStringValue calls the sorter's string converter.

![](img/7dd923a566750151a3aab0dacd0cdaa5_647_0.png)

Figure 10.12 A table with cell renderers

```
table.setDefaultRenderer(Color.class, new ColorTableCellRenderer());
```

That renderer is now used for all objects of the given type in this table.

If you want to select a renderer based on some other criterion, you need to subclass the JTable class and override the getCellRenderer method.

> **TIP:** If your renderer simply draws a text string or an icon, you can extend the DefaultTableCellRenderer class. It takes care of rendering the focus and selection status for you.

### 10.2.4.2 Rendering the Header

To display an icon in the header, set the header value:

```
moonColumn.setHeaderValue(new ImageIcon("Moons.gif"));
```

However, the table header isn't smart enough to choose an appropriate renderer for the header value. You have to install the renderer manually. For example, to show an image icon in a column header, call

```
moonColumn.setHeaderRenderer(table.getDefaultRenderer(ImageIcon.class));
```

### 10.2.4.3 Editing Cells

To enable cell editing, the table model must indicate which cells are editable by defining the `isCellEditable` method. Most commonly, you will want to make certain columns editable. In the example program, we allow editing in four columns.

```java
public boolean isCellEditable(int r, int c)
{
    return c == PLANET_COLUMN || c == MOONS_COLUMN || c == GASEOUS_COLUMN || c == COLOR_COLUMN;
}
```

> **NOTE:** The `AbstractTableModel` defines the `isCellEditable` method to always return `false`. The `DefaultTableModel` overrides the method to always return `true`.

If you run the program (Listings 10.8 to 10.11), note that you can click the check-boxes in the Gaseous column and turn the check marks on and off. If you click a cell in the Moons column, a combo box appears (see Figure 10.13). You will shortly see how to install such a combo box as a cell editor.

![](img/7dd923a566750151a3aab0dacd0cdaa5_648_0.png)

Figure 10.13 A cell editor

Finally, click a cell in the first column. The cell gains focus. You can start typing, and the cell contents change.

What you just saw in action are the three variations of the `DefaultCellEditor` class. A `DefaultCellEditor` can be constructed with a `JTextField`, a `JCheckBox`, or a `JComboBox`. The `JTable` class automatically installs a checkbox editor for Boolean cells and a text field editor for all editable cells that don’t supply their own renderer. The text fields let the user edit the strings that result from applying `toString` to the return value of the `getValueAt` method of the table model.

When the edit is complete, the edited value is retrieved by calling the `getCellEditorValue` method of your editor. That method should return a value of the correct type (that is, the type returned by the `getColumnClass` method of the model).

To get a combo box editor, set a cell editor manually—the `JTable` component has no idea what values might be appropriate for a particular type. For the Moons column, we wanted to enable the user to pick any value between 0 and 20. Here is the code for initializing the combo box:

```
JComboBox moonCombo = new JComboBox();
for (int i = 0; i <= 20; i++)
    moonCombo.addItem(i);
```

To construct a `DefaultCellEditor`, supply the combo box in the constructor:

```
TableCellEditor moonEditor = new DefaultCellEditor(moonCombo);
```

Next, we need to install the editor. Unlike the color cell renderer, this editor does not depend on the object type—we don’t necessarily want to use it for all objects of type `Integer`. Instead, we need to install it into a particular column:

```
moonColumn.setCellEditor(moonEditor);
```

### 10.2.4.4 Custom Editors

Run the example program again and click a color. A color chooser pops up and lets you pick a new color for the planet. Select a color and click OK. The cell color is updated (see Figure 10.14).

The color cell editor is not a standard table cell editor but a custom implementation. To create a custom cell editor, implement the `TableCellEditor` interface. That interface is a bit tedious, and as of Java SE 1.3, an `AbstractCellEditor` class is provided to take care of the event handling details.

The `getTableCellEditorComponent` method of the `TableCellEditor` interface requests a component to render the cell. It is exactly the same as the `getTableCellRendererComponent` method of the `TableCellRenderer` interface, except that there is no focus parameter. When the cell is being edited, it is presumed to have focus. The editor component temporarily replaces the renderer when the editing is in progress. In our example, we return a blank panel that is not colored. This is an indication to the user that the cell is currently being edited.
