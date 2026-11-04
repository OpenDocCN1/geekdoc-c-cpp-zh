# Look-and-Feel Observation 15.1

Buttons can have access shortcuts. Place the & symbol immediately before the desired character in the Button’s text. To press the button by using its access key in the running app, the user presses Alt key to display the underlined character. If the underline is not visible when the app runs, press the Alt key to display the underlines.

You can remove a menu item by selecting it and pressing the Delete key. Menu items can be grouped logically by separator bars, which are inserted by right clicking the menu and selecting Insert > Separator or by typing “—” for the text of a menu item.

In addition to text, Visual Studio allows you to easily add TextBoxes and ComboBoxes (drop-down lists) as menu items. When adding an item in Design mode, you may have noticed that you enter your text for a new item, you’re provided with a drop-down list. Clicking the down arrow (Fig. 15.5) allows you to select the type of item to add—MenuItem (of type ToolStripMenuItem, the default), ComboBox (of type ToolStripComboBox) and TextBox (of type ToolStripTextBox). We focus on ToolStripMenuItems. [Note: If you view this drop-down list for menu items that are not on the top level, a fourth option appears, allowing you to insert a separator bar.]

![](bbox=[0.353, 0.433, 0.646, 0.713])

**Fig. 15.5** | Menu-item options.

ToolStripMenuItems generate a Click event when selected. To create an empty Click event handler, double click the menu item in Design mode. Common actions in response to these events include displaying dialogs and setting properties. Common menu properties and a common event are summarized in Fig. 15.6.

# Look-and-Feel Observation 15.2

It’s a convention to place an ellipsis (...) after the name of a menu item (e.g., Save As...) that requires the user to provide more information—typically through a dialog. A menu item that produces an immediate action without prompting the user for more information (e.g., Save) should not have an ellipsis following its name.