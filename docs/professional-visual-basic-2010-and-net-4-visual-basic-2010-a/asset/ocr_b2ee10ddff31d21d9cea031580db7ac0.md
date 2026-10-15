These controls are actually subclasses of the ToolStrip, so much of the information you learned earlier in this chapter about working with the ToolStrip also applies to the MenuStrip and ContextMenuStrip. When dragged onto the form, these controls appear in the component tray just as the ToolStrip does, and you access the designer for these controls the same way you do for the ToolStrip. However, because these are menus, the most common way to add items is to type them directly into the menu designer that appears when the control is highlighted.

The menu designer is extremely intuitive — the menu appears on your form just as it would at runtime, and you simply fill in the menu items you need. Each item can be renamed, and each can have a Click event associated with it.

# Adding Standard Items to a Menu

If your form’s menu needs to have the standard top-level options (File, Edit, and so on) and the typical options under these items, then you can have all these usual options inserted for you automatically.

To see this capability in action, drag a MenuStrip to a form and then click the smart tag (the right arrow at the right edge) for the MenuStrip to bring up the Items Collection Editor. Click the Insert Standard Items link at the bottom of the dialog.

# Icons and Checkmarks for Menu Items

Each menu item has an Image property. Setting this property to an image causes the image to appear on the left side of the text for the menu option. You can see this property in use by looking at the standard items inserted in the preceding example. The File ▸ Save option has an icon of a diskette, which is produced by setting the image property of that item.

Items can also have check marks beside them. This is done by changing the Checked property of the item to True. You can do this at design time or runtime, enabling you to manipulate the check marks on menus as necessary.

# Context Menus

To implement a context menu for a form or any control on a form, drag a ContextMenuStrip to the form and add the menu items. Items are added and changed the same way as they are with the MenuStrip.

To hook a context menu to a control, set the control’s ContextMenuStrip property to the ContextMenuStrip menu control you want to use. Then, when your program runs and you right-click in the control, the context menu will pop up.

# Dynamically Manipulating Menus at Runtime

Menus can be adjusted at runtime using code. Context menus, for instance, may need to vary according to the state of your form. The following walk-through shows how to add a new menu item to a context menu and how to clear the menu items.

Create a new Windows application. On the blank Form1 for the project, drag over a MenuStrip control. Using the menu designer, type in a top-level menu option of File. Under that option, type in options for Open and Save.

Now place a button on the form. Double-click the button to get its Click event, and place the following code into the event:

```
Dim NewItem As New ToolStripMenuItem
NewItem.Text = "Save As"
' Set any other properties of the menu item you like.
FileToolStripMenuItem.DropDownItems.Add(NewItem)
AddHandler NewItem.Click, _
    AddressOf Me.NewMenuItem_Click
```