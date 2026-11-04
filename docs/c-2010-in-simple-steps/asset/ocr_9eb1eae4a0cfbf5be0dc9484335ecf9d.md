The ToolStripItem class and its derived classes have several properties, methods, and events that you can use to work with the tool strip items. Table 6.4 lists noteworthy properties of the ToolStripItem class:

**Table 6.4: Noteworthy Properties of the ToolStripItem Class**

| Property | Description |
|---|---|
| Alignment | Retrieves or sets a value that signifies whether the item aligns towards the start or the end of the ToolStrip control |
| Anchor | Retrieves or sets the edges of the container to which a tool strip item is bound |
| AutoSize | Retrieves or sets a value signifying whether an item is automatically resized |
| AutoToolTip | Retrieves or sets a value indicating whether to use the Text property or the ToolTipText property for the ToolStripItem ToolTip |
| Available | Retrieves or sets a value indicating whether the tool strip item should be placed in a ToolStrip control |
| CanSelect | Retrieves a value indicating whether an item can be selected |
| DisplayStyle | Retrieves or sets a value indicating whether or not the text and images are displayed on a tool strip item |
| Dock | Retrieves or sets which tool strip item border is docked to its parent control and determines how tool strip item is resized with its parent |
| Image | Retrieves or sets the image displayed on tool strip item |
| Margin | Retrieves or sets the space between two adjacent tool strip items |
| Name | Retrieves or sets the name of a tool strip item |
| Text | Retrieves or sets the text that is to be displayed on a tool strip item |
| TextDirection | Retrieves the orientation of text used on a tool strip item |
| ToolTipText | Retrieves or sets the text that appears as a ToolTip for a control |
| Visible | Retrieves or sets a value specifying whether a tool strip item is displayed |

Table 6.5 lists noteworthy methods of the ToolStripItem class:

**Table 6.5: Noteworthy Methods of the ToolStripItem Class**

| Method | Description |
|---|---|
| DoDragDrop | Starts a drag-and-drop operation |
| GetCurrentParent | Retrieves a ToolStrip control that contains the current tool strip item |
| PerformClick | Activates a tool strip item when its Click event occurs |
| Select | Selects an item in the ToolStrip control |

Table 6.6 lists noteworthy events of the ToolStripItem class:

**Table 6.6: Noteworthy Events of the ToolStripItem Class**

| Event | Description |
|---|---|
| AvailableChanged | Occurs when there is a change in the value of the Available property |
| Click | Occurs when a user clicks a tool strip item |
| DisplayStyleChanged | Occurs when there is a change in the value of the DisplayStyle property |
| OwnerChanged | Occurs when the owner of the tool strip item changes |
| TextChanged | Occurs when the Text property of the tool strip item changes |