# Accessing Data Sources in a Windows Forms Application

This creates an array containing the text that is to appear as column headers in the control. You can add these headers to the control by adding the following code to the constructor:

```
dataGridView->ColumnCount = headers->Length;        // Set number of columns
for(int i = 0; i->headers->Length; i++)
    dataGridView->Columns[i]->Name = headers[i];
```

The first statement specifies the number of columns in the control by setting the value of the ColumnCount property; this also establishes the control in unbound mode. The for loop sets the Name property for each column object to the corresponding string in the headers array. The Columns property for the control returns a reference to the collection of columns, and you just index this to reference a particular column.

You can add the rows to the control in another loop:

```
for each(array<Object^>^ book in books)
    dataGridView->Rows->Add(book);
```

The for each loop selects each of the elements from the books array in turn add passes it to the Add() method for the reference returned by the Rows property for the control. Each element in the books array is an array of strings, and there are as many strings in the array as there are columns in the control.

The control has now been loaded with the data, so the number of rows and columns is determined and the contents of the column headers have been specified. You can now set about customizing the appearance of the control.

# Setting Up the Control

You want the control to be docked in the client area of the form, and you can do this by setting the value of the Dock property:

```
dataGridView->Dock = DockStyle::Fill;
```

The Dock property must be set to one of the constants defined by the DockStyle enumeration; other possible values are Top, Bottom, Left, Right, or None, and these specify the sides of the control that are docked.

You can also relate the position of the control to the client area of the form by setting the Anchor property for the control. The value of Anchor property specifies the edges of the control that are to be attached to the client area of the form. The value is a bitwise combination of the constants defined by the AnchorStyles enumeration and can be any or all of Top, Bottom, Left, and Right. For example to anchor the top and left sides of the control, you would specify the value as AnchorStyles::Top & AnchorStyles::Left. Setting the Anchor property fixes the position of the control plus its scrollbars within the container at a given size, so when you resize the application, window the control and its scrollbars remain at a fixed size. If you set the Dock property as in the previous statement, resizing the application window exposes more or less of the control and the scrollbars adjust accordingly, so that is much better in this case.

You want the width of the columns to be adjusted to accommodate the data in the cells, and you can put this into effect by calling the AutoResizeColumns() function:

```
dataGridView->AutoResizeColumns();
```