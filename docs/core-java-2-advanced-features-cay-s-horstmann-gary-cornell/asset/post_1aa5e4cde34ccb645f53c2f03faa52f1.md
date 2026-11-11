
The `getValueAt` method computes the appropriate value and formats it:

```java
public Object getValueAt(int r, int c)
{
   double rate = (c + minRate) / 100.0;
   int periods = r;
   double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, periods);
   return String.format("%.2f", futureBalance);
}
```

The `getRowCount` and `getColumnCount` methods simply return the number of rows and columns:

```java
public int getRowCount() { return years; }
public int getColumnCount() { return maxRate - minRate + 1; }
```

If you don’t supply column names, the `getColumnName` method of the `AbstractTableModel` names the columns A, B, C, and so on. To change the default column names, override the `getColumnName` method. In this example, we simply label each column with the interest rate.

```java
public String getColumnName(int c) { return (c + minRate) + "%"; }
```

You can find the complete source code in Listing 10.6.

### Listing 10.6 tableModel/InvestmentTable.java

```java
package tableModel;

import java.awt.*;

import javax.swing.*;
import javax.swing.table.*;

/**
 * This program shows how to build a table from a table model.
 * @version 1.03 2006-05-10
 * @author Cay Horstmann
 */
public class InvestmentTable
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
      {
         JFrame frame = new InvestmentTableFrame();
         frame.setTitle("InvestmentTable");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * This frame contains the investment table.
 */
class InvestmentTableFrame extends JFrame
{
   public InvestmentTableFrame()
   {
      TableModel model = new InvestmentTableModel(30, 5, 10);
      JTable table = new JTable(model);
      add(new JScrollPane(table));
      pack();
   }
}

/**
 * This table model computes the cell entries each time they are requested. The table contents
 * shows the growth of an investment for a number of years under different interest rates.
 */
class InvestmentTableModel extends AbstractTableModel
{
   private static double INITIAL_BALANCE = 100000.0;

   private int years;
   private int minRate;
   private int maxRate;

   /**
    * Constructs an investment table model.
    * @param y the number of years
    * @param r1 the lowest interest rate to tabulate
    * @param r2 the highest interest rate to tabulate
    */
   public InvestmentTableModel(int y, int r1, int r2)
   {
      years = y;
      minRate = r1;
      maxRate = r2;
   }

   public int getRowCount()
   {
      return years;
   }

   public int getColumnCount()
   {
      return maxRate - minRate + 1;
   }

   public Object getValueAt(int r, int c)
   {
      double rate = (c + minRate) / 100.0;
      int nperiods = r;
      double futureBalance = INITIAL_BALANCE * Math.pow(1 + rate, nperiods);
      return String.format("$%.2f", futureBalance);
   }

   public String getColumnName(int c)
   {
      return (c + minRate) + "%";
   }
}
```

**javax.swing.table.TableModel 1.2**

| Method | Description |
|---|---|
| `int getRowCount()` | gets the number of rows in the table model. |
| `int getColumnCount()` | gets the number of columns in the table model. |
| `Object getValueAt(int row, int column)` | gets the value at the given row and column. |
| `void setValueAt(Object newValue, int row, int column)` | sets a new value at the given row and column. |
| `boolean isCellEditable(int row, int column)` | returns true if the cell at the given row and column is editable. |
| `String getColumnName(int column)` | gets the column title. |

## 10.2.3 Working with Rows and Columns

In this subsection, you will see how to manipulate the rows and columns in a table. As you read through this material, keep in mind that a Swing table is quite asymmetric—the operations that you can carry out on rows and columns are different. The table component was optimized to display rows of information with the same structure, such as the result of a database query, not an arbitrary two-dimensional grid of objects. You will see this asymmetry throughout this subsection.

### 10.2.3.1 Column Classes

In the next example, we again display our planet data, but this time we want to give the table more information about the column types. This is achieved by defining the method

```
Class<?> getColumnClass(int columnIndex)
```

of the table model to return the class that describes the column type.

The JTable class uses this information to pick an appropriate renderer for the class. Table 10.1 shows the default rendering actions.

You can see the checkboxes and images in Figure 10.9. (Thanks to Jim Evins, www.snaught.com/Jim'sCoolIcons/Planets, for providing the planet images!)

![](img/7dd923a566750151a3aab0dacd0cdaa5_629_0.png)

**Figure 10.9** A table with planet data

### Table 10.1 Default Rendering Actions

| Type | Rendered As |
|---|---|
| Boolean | Checkbox |
| Icon | Image |
| Object | String |

To render other types, you can install a custom renderer—see Section 10.2.4, “Cell Rendering and Editing,” on p. 626.

### 10.2.3.2 Accessing Table Columns

The JTable class stores information about table columns in objects of type TableColumn. A TableColumnModel object manages the columns. (Figure 10.10 shows the relationships among the most important table classes.) If you don’t want to insert or remove columns dynamically, you won’t use the column model much. The most common use for the column model is simply to get a TableColumn object:

```
int columnIndex = . . .;
TableColumn column = table.getColumnModel().getColumn(columnIndex);
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_630_0.png)

**Figure 10.10** Relationship between table classes

### 10.2.3.3 Resizing Columns

The TableColumn class gives you control over the resizing behavior of columns. You can set the preferred, minimum, and maximum width with the methods

```
void setPreferredWidth(int width)
void setMinWidth(int width)
void setMaxWidth(int width)
```

This information is used by the table component to lay out the columns.

Use the method

```
void setResizable(boolean resizable)
```

to control whether the user is allowed to resize the column.

You can programmatically resize a column with the method

```
void setWidth(int width)
```

When a column is resized, the default is to leave the total size of the table unchanged. Of course, the width increase or decrease of the resized column must then be distributed over other columns. The default behavior is to change the size of all columns to the right of the resized column. That’s a good default because it allows a user to adjust all columns to a desired width, moving from left to right.

You can set another behavior from Table 10.2 by using the method

```
void setAutoResizeMode(int mode)
```

of the JTable class.

### Table 10.2 Resize Modes

| Mode | Behavior |
|---|---|
| `AUTO_RESIZE_OFF` | Don’t resize other columns, change the table width. |
| `AUTO_RESIZE_NEXT_COLUMN` | Resize the next column only. |
| `AUTO_RESIZE_SUBSEQUENT_COLUMNS` | Resize all subsequent columns equally; this is the default behavior. |
| `AUTO_RESIZE_LAST_COLUMN` | Resize the last column only. |
| `AUTO_RESIZE_ALL_COLUMNS` | Resize all columns in the table; this is not a good choice because it prevents the user from adjusting multiple columns to a desired size. |

### 10.2.3.4 Resizing Rows

Row heights are managed directly by the JTable class. If your cells are taller than the default, you may want to set the row height:

```
table.setRowHeight(height);
```

By default, all rows of the table have the same height. You can set the heights of individual rows with the call

```
table.setRowHeight(row, height);
```

The actual row height equals the row height set with these methods, reduced by the row margin. The default row margin is 1 pixel, but you can change it with the call

```
table.setRowMargin(margin);
```

### 10.2.3.5 Selecting Rows, Columns, and Cells

Depending on the selection mode, the user can select rows, columns, or individual cells in the table. By default, row selection is enabled. Clicking inside a cell selects the entire row (see Figure 10.9 on p. 629). Call

```
table.setRowSelectionAllowed(false)
```

to disable row selection.

When row selection is enabled, you can control whether the user is allowed to select a single row, a contiguous set of rows, or any set of rows. You need to retrieve the selection model and use its setSelectionMode method:

```
table.getSelectionModel().setSelectionMode(mode);
```

Here, mode is one of the three values:
