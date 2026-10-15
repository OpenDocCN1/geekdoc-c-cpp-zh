
Loading this control means loading items into the left list box, which we will call `SourceListBox`. Getting selected items back out involves exposing the items that are selected in the right list box, named `TargetListBox`.

The buttons in the middle that transfer elements back and forth are called `AddButton`, `AddAllButton`, `RemoveButton`, and `ClearButton`, from top to bottom, respectively.

There are several ways to handle this kind of interface element in detail. A production-level version would have the following characteristics:

- Buttons would gray out (disable) when they are not appropriate. For example, `btnAdd` would not be enabled unless an item were selected in `lstSource`.
- Items could be dragged and dropped between the two list boxes.
- Items could be selected and moved with a double-click.

Such a production-type version contains too much code to discuss in this chapter. For simplicity, the exercise has the following limitations:

- Buttons do not gray out when they should be unavailable.
- Drag-and-drop is not supported. (Implementation of drag-and-drop is discussed in Chapter 14, if you are interested in adding it to the example.)
- No double-clicking is supported.

This leaves the following general tasks to make the control work, which are detailed in the step-by-step exercise that follows:

- 1. Create a `UserControl` and name it `ListSelector`.
- 2. Add the list boxes and buttons to the `ListSelector` design surface, using a `TableLayoutPanel` and a `FlowLayoutPanel` to control layout when the control is resized.
- 3. Add logic to transfer elements back and forth between the list boxes when buttons are pressed. (More than one item may be selected for an operation, so several items may need to be transferred when a button is pressed.)
- 4. Expose properties to enable the control to be loaded, and for selected items to be fetched by the form that contains the control.

## Resizing the Control

As shown in Figure 15-3, there are three main areas of the control: the two `ListBox` controls and a vertical strip between them that holds the buttons. As the control is resized, these areas need to also be appropriately resized.

If the `ListSelector` control gets too small, then there won't be enough room for the buttons and the list boxes to display properly, so it needs to have a minimum size. That's enforced by setting the `MinimumSize` property for the `UserControl` in the designer. The `MinimumSize` property is inherited from the `Control` class (as discussed in the previous chapter).

The rest of the resizing is handled by using a `TableLayoutPanel` that contains three columns, one for each of the three areas. That is, the first column of the `TableLayoutPanel` will hold `SourceListBox`, the second column will hold the buttons, and the third column will hold `TargetListBox`. The capabilities of the `TableLayoutPanel` enable the middle column to be a fixed size, and the left and right columns to share all remaining width.

The middle column could contain a standard `Panel` to hold the buttons, but it's a bit easier to use a `FlowLayoutPanel` because it automatically stacks the buttons.

## Exposing Properties of Contained Controls

Most of the controls contained in the composite control in this exercise do not need to expose their interfaces to the form that will use the composite control. The buttons, for example, are completely private to the `ListSelector` — none of their properties or methods need to be exposed.

The easiest way to load up the control is to expose the Items property of the source list box. Similarly, the easiest way to allow access to the selected items is to expose the Items property of the target list box. The Items property exposes the entire collection of items in a list box, and can be used to add, clear, or examine items. No other properties of the list boxes need to be exposed.

The exercise also includes a Clear method that clears both list boxes simultaneously. This allows the control to be easily flushed and reused by a form that consumes it.

## Stepping through the Example

Here is the step-by-step procedure to build the composite UserControl:

- 1. Start a new Windows Control Library project and name it ListSelector.
- 2. Right-click on the UserControl1.vb module that is generated for the project and select Rename. Change the name of the module to ListSelector.vb. The resulting dialog asks if you wish to rename all references in the project. Click Yes. This automatically changes the name of your class to ListSelector.
- 3. Go to the design surface for the control. Increase the size of the control to about 300 × 200. Then drag a TableLayoutPanel onto the control and set the Dock property of the TableLayoutPanel to Fill.
- 4. Click the smart tag (the triangular glyph in the upper-right corner) of the TableLayoutPanel. A menu will appear. Select Edit Rows and Columns.
- 5. Highlight Column2 and click the Insert button. The TableLayoutPanel will now have three columns. In the new column just inserted (the new Column2), the width will be set to an absolute size of 20 pixels. Change that width to 100 pixels. The dialog containing your column settings should now look like Figure 15-4.
- 6. Click the Show drop-down menu in the upper-left corner and select Rows. Press the Delete button to delete a row because you need only one row in the control. Click OK. The design surface for the control should now look similar to Figure 15-5.
- 7. Drag a ListBox into the first cell and another one into the third cell. Drag a FlowLayoutPanel into the middle cell. For all three of these, set the Dock property to Fill.
- 8. Drag four buttons into the FlowLayoutPanel in the middle. At this point your control should look like the one shown in Figure 15-6.

![](img/d99870e80390742f93963da7be0b2e61_598_0.png)

![](img/d99870e80390742f93963da7be0b2e61_598_1.png)

![](img/d99870e80390742f93963da7be0b2e61_598_2.png)

### 9.

Change the names and properties of these controls as shown in the following table:

| ORIGINAL NAME | NEW NAME | PROPERTIES TO SET FOR CONTROL |
|---|---|---|
| ListBox1 | SourceListBox | |
| ListBox2 | TargetListBox | |
| Button1 | AddButton | Text = "Add >"<br>Size.Width = 90 |
| Button2 | AddAllButton | Text = "Add All >>"<br>Size.Width = 90 |
| Button3 | RemoveButton | Text = "< Remove"<br>Margin.Top = 20<br>Size.Width = 90 |
| Button4 | ClearButton | Text = "<< Clear"<br>Size.Width = 90 |

### 10.

In the Properties window, click the drop-down at the top and select ListSelector so that the properties for the UserControl itself appear in the Properties window. Set the MinimumSize height and width to 200 pixels each.

### 11.

Create the public properties and methods of the composite control. In this case, you need the following members:

| MEMBER | DESCRIPTION |
|---|---|
| Clear method | Clears both list boxes of their items |
| SourceItems property | Exposes the Items collection for the source list box |
| SelectedItems property | Exposes the Items collection for the target list box |

The code for these properties and methods is as follows:

```
```vb
< Browsable(False) >
Public ReadOnly Property SourceItems() As ListBox.ObjectCollection
    Get
        Return SourceListBox.Items
    End Get
End Property
< Browsable(False) >
Public ReadOnly Property SelectedItems() As ListBox.ObjectCollection
    Get
        Return TargetListBox.Items
    End Get
End Property
Public Sub Clear()
    SourceListBox.Items.Clear()
    TargetListBox.Items.Clear()
End Sub
```
```

Remember that your class must have an Imports for System.ComponentModel at the top so that the attributes can be identified by the compiler.

### 12.

Put logic in the class to transfer items back and forth between the list boxes and clear the target list box when the Clear button is pressed. This logic manipulates the collections of items in the list boxes, and is fairly brief. You need one helper function to check whether an item is already in a list box before adding it (to avoid duplicates). Here are the Click events for each of the buttons, with the helper function at the top:

```
```vb
Private Function ItemInListBox(ByVal ListBoxToCheck As ListBox,
                               ByVal ItemToCheck As Object) As Boolean
    Dim bFound As Boolean = False
```
```
