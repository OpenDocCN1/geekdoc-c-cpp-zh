This pop-up menu is called the Smart Tasks panel. When it appears, it gives you access to the common controls of the control it belongs to. In the case of the DropDownList, you get three options. The first option enables you to bind the control to a data source, which is demonstrated in Chapter 13. The second item enables you to manually add items to the list, and the last option sets the AutoPost property of the control. With this option checked, the control submits the page in which it is backed to the server as the user chooses a new item from the list. Note that the browser must have JavaScript enabled for this to work.

The Smart Tasks panel appears only for the complex controls that have a lot of features. It won't seem for simple controls like Button or Label. To reopen the Smart Tasks panel, right-click the control in the designer and choose Smart Tag. Alternatively, click the small arrow at the top-right corner of the control, or press Shift+Alt+F10 when the control is selected. You can also open the Smart Tasks panel from markup view. Simply click anywhere on the opening or closing tag of a control or other piece of markup and press Ctrl+Dot (Ctrl+.). Alternatively, hover over the blue rectangle at the Smart Tasks panel of the DropDropDownList, click the grey arrow that appears.

On the Smart Tasks panel of the DropDownList, click the Edit Items to bring up the ListItem Collection Editor, in Figure 4-7.

![](bbox=[0.118, 0.439, 0.552, 0.672])

FIGURE 4-7

This dialog box enables you to add new items to the list control. You add them through window are added as <asp:ListItem> elements within the tags for the control.

+   4. Click the Add button on the left side of the screen to insert a new list item. Then in the Properties Grid on the right, enter C for the Text property and press Tab. As soon as you tab away from the Text property, the value is copied to the Value property as well. This is convenient if you want both the Text and the Value property to be the same. However, it's perfectly OK (and quite common) to assign a different value to the Value property.
5. Repeat step 4 twice, this creating list items for Visual Basic and CSS. You can use the up and down buttons in the middle of the dialog box to change the order of the items in the list.