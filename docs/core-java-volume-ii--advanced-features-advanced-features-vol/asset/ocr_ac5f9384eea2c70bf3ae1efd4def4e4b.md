When a column is resized, the default is to leave the total size of the table unchanged. Of course, the width increase or decrease of the resized column must then be distributed over other columns. The default behavior is to change the size of all columns to the right of the resized column. That’s a good default because it allows a user to adjust all columns to a desired width, moving from left to right.

You can set another behavior from Table 11.2 by using the method

```
void setAutoResizeMode(int mode)
```

of the JTable class.

**Table 11.2  Resize Modes**

| Mode | Behavior |
|---|---|
| `AUTO_RESIZE_OFF` | Don’t resize other columns; change the table width. |
| `AUTO_RESIZE_NEXT_COLUMN` | Resize the next column only. |
| `AUTO_RESIZE_SUBSEQUENT_COLUMNS` | Resize all subsequent columns equally; this is the default behavior. |
| `AUTO_RESIZE_LAST_COLUMN` | Resize the last column only. |
| `AUTO_RESIZE_ALL_COLUMNS` | Resize all columns in the table; this is not a good choice because it prevents the user from adjusting multiple columns to a desired size. |

# 11.1.3.4 Resizing Rows

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