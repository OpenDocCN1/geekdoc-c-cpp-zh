# AN INTRODUCTION TO C GUI PROGRAMMING

Having created the menu, we use gtk_menu_item_set_submenu to set it as a submenu of the 'File' menu item.

```
gtk_menu_item_set_submenu (GTK_MENU_TREE(file_mi), f_menu);
```

At this point, we have a menu bar with the 'File' item on, and an empty menu as the submenu of that menu item We create a new menu to hold the 'Quit' option, and we use gtk_menu_shell_append to add this to the 'File' menu.

```
GtkWidget *quit_mi = gtk_menu_item_new_with_label("Quit");
gtk_menu_shell_append(GTK_MENU_SHELL(menu), quit_mi);
```

We have a menu bar with a single menu ('File') which contains a single option ('Quit'), but as yet that option doesn't do anything. To make the menu item do something, we connect a handler callback to activate signal with connect, just as with a button

The code to connect our existing end_program handler to the 'Quit' menu item is:

```
GSignal connect(quit_mi, "activate", CALLBACK(end_program), NULL);
```

That's it - you now have a working Quit menu option in your application. You can use the same process to add as many menus and menu items as you want to a menu bar.

![](bbox=[0.055, 0.612, 0.845, 0.775])

+   - A GtkMenuBar with a single menu (File) containing a Quit item

Note that the function we used to add a menu to the menu bar was called gtk_menu_item_set_submenu - effectively, the menu is regarded as a submenu of the top-level menu item in the menu bar You can use exactly the same function to create an actual sub-menu from a menu item in, and can nest these calls as deeply as you want to create the sort of hierarchical menu structure that more complex applications use.