# The Items Collection Editor for an enhanced ToolStrip control

Items Collection Editor

![](bbox=[0.062, 0.106, 0.755, 0.383])

| ToolToolTip | ToolToolTip | |
| --- | --- | --- |
| | | CheckStyle | Unchecked |
| Button | Add | TextStyle | Text |
| Member | | Font | Segoe UI |
| fill,Customer:ID | | Color | System.Drawing.Bitmap |
| A customer:ToolTipLabel | ImageName | MiddleCenter |
| customer:ToolTipButton | ImageScaling | Size |
| ToolStripSeparator | ImageTransparentColor | Magenta |
| ToolToolTip | RightLeft | No |
| | RightLeftAutoMinimum | Get All Customers |
| | Text | MiddleCenter |
| | Direction | Horizontal |
| | TagRelation | ImageForText |
| | Behavior | True |

# Common properties of ToolStrip items

| Property | Description |
| --- | --- |
| DisplayStyle | Indicates whether a button displays an image, text, or both an image and text. |
| Image | The image that's displayed on a button if you select Image or ImageAnd for the DisplayStyle property. |
| Text | The text that's displayed on a button if you select Text or ImageAnd for the DisplayStyle property. |
| Width | The width of the item.

# Description

+   - To display the Items Collection Editor dialog box, display the smart tag menu for the ToolStrip and select the Edit Items command.
- To add an item, select the type of control you want to add from the combo bar and click the Add button. To add a separator bar, choose Separator. You can also add an item using the drop-down list that's displayed when the ToolStrip is in the Form Designer.
- To move an item, select the item in the Members list and click the up and down arrows to the right of the list.
- To delete an item, select it in the Members list and click the Delete button to the right of the list.
- To set the properties for an item, select the item in the Members list and use the Properties list on the right side of the dialog box to set the properties. You can also set the properties of an item by selecting it in the Form Designer and then using the Properties window.

# Note

+   - Because the BindingNavigator control is a ToolStrip control, you can use the Items Collection Editor to work with it like any other ToolStrip control.

Figure 19-6 How to use the Items Collection Editor