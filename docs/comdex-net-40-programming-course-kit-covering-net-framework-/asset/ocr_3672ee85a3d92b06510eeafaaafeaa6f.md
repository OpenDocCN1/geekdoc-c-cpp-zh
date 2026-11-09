be selected by the user and contain submenus, which are menus with different sets of options. The **MenuStrip** class, which is placed inside the **System.Windows.Forms** namespace, provides the functionality for the **MenuStrip** control. Table 4.7 lists the noteworthy properties of the **MenuStrip** class:

**Table 4.7: Noteworthy Properties of the MenuStrip Class**

| Property | Description |
|---|---|
| CanOverflow | Returns or sets a value that indicates whether the **MenuStrip** control supports overflow functionality |
| ShowItemToolTips | Returns or sets a value that indicates whether tooltips appear for the **MenuStrip** control |
| Stretch | Returns or sets a value that indicates whether the **MenuStrip** control stretches from one end to another end in its container |

Table 4.8 is the noteworthy events of the MenuStrip class:

**Table 4.8: Noteworthy Events of the MenuStrip Class**

| Event | Description |
|---|---|
| MenuActivate | Occurs when the user accesses the menu |
| MenuDeactivate | Occurs when the **MenuStrip** control is deactivated |

The **MenuStrip** control is only a container for the menus. After adding a **MenuStrip** control in a Windows Forms application, you need to add the menus and their menu items manually. You can also add separators to menu items, assign shortcut keys for menu and menu items, display check marks for menu items, and create submenus.

You can also add access keys to menus and menu items. An access key is a character that you can use with the ALT key to access or select a menu or menu item. To specify an access key for a menu or menu item, you need to prefix the character, which you want to make the access key, with an ampersand (&) in the Text property of the menu or menu item. The access key appears underlined in the menu or menu item name. For example, if you specify the Text property of the File menu as &File, then f (or F) becomes the access key for the File menu.

![](bbox=[0.209, 0.572, 0.264, 0.612])

> > The menus and menu items are generally represented as objects of the **ToolStripMenuItem** class.

Some properties and events are common to the menus and menu items. Table 4.9 lists noteworthy common properties of the menus and menu items:

**Table 4.9: Noteworthy Common Properties of the Menus and Menu Items**

| Property | Description |
|---|---|
| Checked | Returns or sets a value that indicates whether the menu (or menu item) object is checked |
| CheckOnClick | Returns or sets a value specifying whether the menu (or menu item) object automatically appears checked or unchecked when clicked |
| CheckState | Returns or sets a value that indicates whether the menu (or menu item) is in the checked, unchecked, or indeterminate state |
| Enabled | Returns or sets a value that indicates whether the menu (or menu item) is enabled |
| ShortcutKeys | Returns or sets the shortcut keys associated with the menu (or menu item) |
| ShowShortcutKeys | Returns or sets a value that indicates whether the shortcut keys associated with the menu (or menu item) are displayed next to it |