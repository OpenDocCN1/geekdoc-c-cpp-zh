# Listing 11.7 *(Continued)*

```
```java
colorChooser.setColor((Color) value);
return panel;
}

public boolean shouldSelectCell(EventObject anEvent)
{
    // start editing
    colorDialog.setVisible(true);

    // tell caller it is ok to select this cell
    return true;
}

public void cancelCellEditing()
{
    // editing is canceled--hide dialog
    colorDialog.setVisible(false);
    super.cancelCellEditing();
}

public boolean stopCellEditing()
{
    // editing is complete--hide dialog
    colorDialog.setVisible(false);
    super.stopCellEditing();

    // tell caller it is ok to use color value
    return true;
}

public Object getCellEditorValue()
{
    return colorChooser.getColor();
}
```
```

| javax.swing.JTable 1.2 |
|---|
| • `TableCellRenderer getDefaultRenderer(Class<?> type)`<br>gets the default renderer for the given type. |
| • `TableCellEditor getDefaultEditor(Class<?> type)`<br>gets the default editor for the given type. |