# 9.

Change the names and properties of these controls as shown in the following table:

| ORIGINAL NAME | NEW NAME | PROPERTIES TO SET FOR CONTROL |
|---|---|---|
| ListBox1 | SourceListBox | |
| ListBox2 | TargetListBox | |
| Button1 | AddButton | Text = "Add >"<br>Size.Width = 90 |
| Button2 | AddAllButton | Text = "Add All >>"<br>Size.Width = 90 |
| Button3 | RemoveButton | Text = "< Remove"<br>Margin.Top = 20<br>Size.Width = 90 |
| Button4 | ClearButton | Text = "<< Clear"<br>Size.Width = 90 |

# 10.

In the Properties window, click the drop-down at the top and select ListSelector so that the properties for the UserControl itself appear in the Properties window. Set the MinimumSize height and width to 200 pixels each.

# 11.

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

# 12.

Put logic in the class to transfer items back and forth between the list boxes and clear the target list box when the Clear button is pressed. This logic manipulates the collections of items in the list boxes, and is fairly brief. You need one helper function to check whether an item is already in a list box before adding it (to avoid duplicates). Here are the Click events for each of the buttons, with the helper function at the top:

```
```vb
Private Function ItemInListBox(ByVal ListBoxToCheck As ListBox,
                               ByVal ItemToCheck As Object) As Boolean
    Dim bFound As Boolean = False
```
```