# How to add menus to a form

To provide access to the functions of an application, you can add menus to a form. Menus sometimes duplicate the functionality that's already available in the buttons and other controls of a form, but they can also provide access to the functions that aren't available anywhere else.

# How to create menus

Visual Studio provides an easy-to-use facility for adding menus to a form. To do that, you start by adding a MenuStrip control to the form as illustrated in figure 24-4. When you add this control, the MainMenuStrip property of the form is automatically set to the name of that control but the control isn't displayed on the form. Instead, it's displayed in the Component Designer at the bottom of the Form Designer.

After you add the MenuStrip control to the form, the Menu Designer is displayed at the top of the form. Then, you can add menus and menu items by typing the text you want to appear in the Menu Designer anywhere it says “Type Here.\ When you type the text for the first menu, additional areas open below and to the right of that menu. As a result, it's easy to enter new menus, submenus, and menu items. With other controls, you can use the ampersand character (&) to provide an access key when you enter the text for the menu item. In addition, you can create a separator bar by using a dash (-) for the menu item's text.

Once you've created the menus and menu items for your application, you can easily right-click on the name of the menu and select the Edit DropDowns--Items command from the shortcut menu. This displays the Items Collection Editor dialog box, which makes it easy to edit the names for each menu item or set any of the other properties for a menu item. This dialog also allows you to add, move, and delete menu items.

When setting the names for each menu item, it's a common convention to use mnu as the prefix for each menu item. For example, you might use mnuActionClear as the name for the Clear item of the Action menu. Otherwise, you can accept the default name that's assigned by the Menu Designer. For example, the default name for the Clear item of the Action menu would be clearToolMenuItem.

If you need to insert a new item in a menu, you can right-click on a menu item to display a shortcut menu. Then, you can select the MenuItem command from the Insert submenu to insert a new item. Or, you can select the Separator command from the Insert submenu to insert a separator bar. In addition, the shortcut menu for a menu item provides Cut, Copy, Paste, and Delete commands.