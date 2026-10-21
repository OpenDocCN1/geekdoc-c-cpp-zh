# Try It Out   The DataGridView Control in Unbound Mode

This example displays a list of books where each book is specified by the ISBN, the title, the author, and the publisher. Create a new Windows Form project with the name Ex22_01. Add a DataGridView control to the form and click the arrow at top-right of the control to displays the pop-up menu show in Figure 22-2.

![](bbox=[0.275, 0.21, 0.83, 0.52])

Figure 22-2

If you click the bottom menu item, Dock in parent container, the control fills the client area of the form. The top menu item is for selecting a data source, but you are not going to specify a data source this time. If you click the AddColumn menu item, the dialog box shown in Figure 22-3 for entering columns to the control is displayed.

The Unbound column radio button is checked because there is no data source identified for the control, which is the way it should be for this example. The Name: entry is the value of the Name property for the column, and the Header Text: entry is the value of the HeaderText property, which corresponds to the text that is shown in the control as the column heading. If you extend the list box that is for selecting the Type: value, you’ll see you have a range of choices for the type of column. Here you should leave it as the default choice — a TextBox column — because you’ll be adding strings as the data to be displayed. The other column types in the list deal with provide for various controls in the cells representing the data:

| DataGridViewButtonColumn | This type is used to display a button in each cell in the column. |
| DataGridViewCheckBoxColumn | This type is used when you want to store bool values (System::Boolean objects) or System::Windows::Forms::CheckState objects as checkboxes in the cells in the column. |

Table continued on following page