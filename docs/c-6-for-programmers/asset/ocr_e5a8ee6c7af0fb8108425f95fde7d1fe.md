Alternatively, you can add items to ListBoxes and CheckedListBoxes visually by examining the Items property in the Properties window. Clicking the ellipsis button opens the String Collection Editor, which contains a text area for adding items; each item appears on a separate line (Fig. 15.17). Visual Studio then writes code to add these strings to the Items collection inside method InitializeComponent.

![](bbox=[0.339, 0.23, 0.65, 0.352])

Fig. 15.17 | String Collection Editor.

Figure 15.18 uses class ListBoxTestForm to add, remove and clear items from ListBox displayListBox. Class ListBoxTestForm uses TextBox inputTextBox to allow the user to type in a new item. When the user clicks the Add Button, the new item appears in displayListBox. Similarly, if the user selects an item and clicks Remove, the item is deleted. When clicked, Clear deletes all entries in displayListBox. The user terminates the app by clicking Exit.

The addButton_Click event handler (lines 20–24) calls method Add of the Items collection in the ListBox. This method takes a string as the item to add to displayListBox. In this case, the string used is the user input from the inputTextBox (line 22). After the item is added, inputTextBox.Text is cleared (line 23).

The removeButton_Click event handler (lines 27–34) uses method RemoveAt to remove an item from the ListBox. Event handler removeButton_Click first uses property SelectedIndex to determine which index is selected. If SelectedIndex is not -1 (i.e., an item is selected), line 32 removes the item that corresponds to the selected index.

```
```csharp
1    // Fig. 15.18: ListBoxTestForm.cs
2    // Program to add, remove and clear ListBox items
3    using System;
4    using System.Windows.Forms;
5
6    namespace ListBoxTest
7    {
8       // Form uses a TextBox and Buttons to add,
9       // remove, and clear ListBox items
10      public partial class ListBoxTestForm : Form
11      {
12         // constructor
13         public ListBoxTestForm()
14         {
```
```

Fig. 15.18 | Program to add, remove and clear ListBox items. (Part 1 of 3.)