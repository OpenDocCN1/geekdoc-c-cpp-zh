
TableLayoutPanel uses a grid structure to control the layout of controls. Any Windows Forms control can be a child of the TableLayoutPanel, including another TableLayoutPanel. This allows for a very flexible and dynamic window design. When a control is added to a TableLayoutPanel, four additional properties are added to the Layout category of the property page. They are Column, ColumnSpan, Row, and RowSpan. Much like an HTML table on a Web page, column and row spans can be set for each control. By default, the control will be centered in the cell of the table, but this can be changed by using the Anchor and Dock properties.

The default style of the rows and columns can be changed using RowStyles and ColumnStyles collections. These collections contain RowStyle and ColumnStyle objects, respectively. The Style objects have a common property, SizeType. SizeType uses the SizeType enumeration to determine how the column width or row height should be sized. Values include AutoSize, Absolute, and Percent. AutoSize shares the space with other peer controls. Absolute allows a set number of pixels for the size and Percent tells the control to size the column or width as a percentage of the parent control.

Rows, columns, and child controls can be added or removed at runtime. The GrowStyle property takes a TableLayoutPanelGrowStyle enumeration value that sets the table to add a column or a row, or stay a fixed size when a new control is added to a full table. If the value is FixedSize, an ArgumentException is thrown when there is an attempt to add another control. If a cell in the table is full and the control will be placed in the empty cell. This property has an effect only when the table is full and a control is added.

The sample code includes a form containing both a flow layout panel and a table layout panel to show the effect of resizing the form on the controls within the panels.

## SplitContainer

The SplitContainer control is really three controls in one. It has two panel controls with a bar or splitter between them. The user is able to move the bar and resize the panels. As the panels resize, the controls in the panels can also be resized. The best example of a SplitContainer is File Explorer. The left panel contains a TreeView of folders, and the right side contains a ListView of folder contents. When the user moves the mouse over the splitter bar, the cursor changes, showing that the bar can be moved. The SplitContainer can contain any control, including layout panels and other SplitContainers. This allows the creation of very complex and sophisticated forms.

The movement and position of the splitter bar can be controlled with the SplitterDistance and SplitterIncrement properties. The SplitterDistance property determines where the splitter starts in relation to the left or top of the control. The SplitterIncrement determines the number of pixels the splitter moves when being dragged. The panels can have their minimum size set with the Panel1MinSize and Panel2MinSize properties. These properties are also in pixels.

The Splitter control raises two events that relate to moving: the SplitterMoving event and the SplitterMoved event. One takes place during the move, and the other takes place after the move has happened. They both receive SplitterEventArgs. SplitterEventArgs contains properties for the X and Y coordinates of the upper-left corner of the Splitter (SplitterX and SplitterY) and the X and Y coordinates of the mouse pointer (X and Y).

## TabControl and TabPages

TabControl allows you to group related controls onto a series of tab pages. TabControl manages the collection of TabPages. Several properties control the appearance of TabControl. The Appearance property uses the TabAppearance enumeration to determine what the tabs look like. The values are FlatButtons, Buttons, or Normal. The Multiline property is a Boolean that determines if more than one row of tabs is shown. If the Multiline property is set to false and there are more tabs than can fit in the display, arrows appear that allow the user to scroll and see the rest of the tabs.

The TabPage Text property is what is displayed on the tab. The Text property is a parameter in a constructor override as well.

Once you create a TabPage control, it is basically a container control in which you can place other controls. The Designer in Visual Studio .NET makes it easy to add TabPage controls to a TabControl control by using the collection editor. You can set the various properties as you add each page. Then you can drag the other child controls to each TabPage control.

You can determine the current tab by looking at the SelectedTab property. The SelectedIndexChanged event is raised each time a new tab is selected. By listening to the SelectedIndexChanged event and then confirming the current tab with SelectedTab, you can do special processing based on each tab. You could, for example, manage the data displayed for each tab.

## ToolStrip

The ToolStrip control is a container control used to create toolbars, menu structures, and status bars. The ToolStrip is used directly for toolbars, and serves as the base class for the MenuStrip and StatusStrip controls.

When used as a toolbar, the ToolStrip control uses a set of controls based on the abstract ToolStripItem class. ToolStripItem adds the common display and layout functionality as well as managing most of the events used by the controls. ToolStripItem is derived from the System.ComponentModel.Component class and not from the Control class. ToolStripItem-based classes must be contained in a ToolStrip-based container.

Image and Text are probably the most common properties that will be set. Images can be set with either the Image property or by using the ImageList control and setting it to the ImageList property of the ToolStrip control. The ImageIndex property of the individual controls can then be set.

Formatting of the text on a ToolStripItem is handled with the Font, TextAlign, and TextDirection properties. TextAlign sets the alignment of the text in relation to the control. This can be any of the ContentAlignment enumeration values. The default is MiddleRight. The TextDirection property sets the orientation of the text. Values can be any of the ToolStripTextDirection enumeration values, which include Horizontal, Inherit, Vertical270, and Vertical90. Vertical270 rotates the text 270 degrees, and Vertical90 rotates the text 90 degrees.

The DisplayStyle property controls whether text, image, text and image, or nothing is displayed on the control. When AutoSize is set to true, the ToolStripItem will resize itself so that only the minimum amount of space is used.

The controls that are derived directly from ToolStripItem are listed in the following table.

| TOOL STRIP ITEMS | DESCRIPTION |
|---|---|
| ToolStripButton | Represents a button that the user can select. |
| ToolStripLabel | Displays nonselectable text or images on the ToolStrip. The ToolStripLabel can also display one or more hyperlinks. |
| ToolStripSeparator | Used to separate and group other ToolStripItems. Items can be grouped according to functionality. |
| ToolStripDropDownItem | Displays drop-down items. Base class for ToolStripDropDownButton, ToolStripMenuItem, and ToolStripSplitButton. |
| ToolStripControlHost | Hosts other non-ToolStripItem-derived controls on a ToolStrip. Base class for ToolStripComboBox, ToolStripProgressBar, and ToolStripTextBox. |

The last two items in the list, ToolStripDropDownItem and ToolStripControlHost, deserve a little more discussion. ToolStripDropDownItem is the base class for ToolStripMenuItems, which are used to build the menu structure. ToolStripMenuItems are added to MenuStrip controls. As mentioned earlier, MenuStrips are derived from ToolStrip controls. This is important when it comes time to manipulate or extend menu items. Because toolbars and menus are derived from the same classes, creating a framework for managing and executing commands is much easier.

ToolStripControlHost can be used to host other controls that do not derive from ToolStripItem. Remember that the only controls that can be directly hosted by a ToolStrip are those that are derived from ToolStripItem.

## MenuStrip

The MenuStrip control is the container for the menu structure of an application. As mentioned earlier, MenuStrip is derived from the ToolStrip class. The menu system is built by adding ToolStripMenuItem objects to the MenuStrip. You can do this in code or in the Designer of Visual Studio. Drag a MenuStrip control onto a form in the Designer and the MenuStrip will allow the entry of the menu text directly on the menu items.

The MenuStrip control has only a couple of additional properties. GripStyle uses the ToolStripGripStyle enumeration to set the grip as visible or hidden. The MdiWindowListItem property takes or returns a ToolStripMenuItem. This ToolStripMenuItem is the menu that shows all open windows in an MDI application.

## ContextMenuStrip

To show a context menu, or a menu displayed when the user right-clicks the mouse, the ContextMenuStrip class is used. Like MenuStrip, ContextMenuStrip is a container for ToolStripMenuItems objects. However, it is derived from ToolStripDropDownMenu. A ContextMenu is created the same way as a MenuStrip. ToolStripMenuItems are added, and the click event of each item is defined to perform a specific task. Context menus are assigned to specific controls. This is done by setting the ContextMenuStrip property of the control. When the user right-clicks the control, the menu is displayed.

## ToolStripMenuItem

ToolStripMenuItem is the class that builds the menu structures. Each ToolStripMenuItem object represents a single menu choice on the menu system. Each ToolStripMenuItem has a ToolStripItemCollection that maintains the child menus. This functionality is inherited from ToolStripDropDownItem.

Because ToolStripMenuItem is derived from ToolStripItem, all of the same formatting properties apply. Images appear as small icons to the right of the menu text. Menu items can have check marks show up next to them with the Checked and CheckState properties.

Shortcut keys can be assigned to each menu item. They are generally two key chords such as Ctrl+C (common shortcut for Copy). When a shortcut key is assigned, it can optionally be displayed on the menu by setting the ShowShortcutKey property to true.

To be useful, the menu item has to do something when the user clicks it or uses the defined shortcut keys. The most common way is to handle the Click event. If the Checked property is being used, the CheckStateChanged and CheckedChanged events can be used to determine a change in the checked state.

## ToolStripManager

Menu and toolbar structures can become large and cumbersome to manage. The ToolStripManager class provides the ability to create smaller, more manageable pieces of a menu or toolbar structure and then combine them when needed. An example of this is a form that has several different controls on it.
