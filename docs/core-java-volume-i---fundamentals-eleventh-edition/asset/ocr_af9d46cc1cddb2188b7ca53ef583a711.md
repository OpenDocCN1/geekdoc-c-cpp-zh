# ### 13.5.3 Menus

We started by introducing the most common controls that you might want to place into a window, such as various kinds of buttons, text fields, and combo boxes. JavaFX also supports another type of user interface element—pull-down menus that are familiar from GUI applications.

*A menu bar at the top of a window contains the names of the pull-down menus. Clicking on a name opens the menu containing menu items and submenus. When the user clicks on a menu item, an action event is triggered. Figure 13.19 shows a typical menu with a submenu.*

![](bbox=[0.22, 0.351, 0.7, 0.507])

**Figure 13.19** A menu with a submenu

You construct a menu item by providing the menu text and, optionally, a graphical decoration. The decoration can be any Node, but it is most common to provide an image.

```
    MenuItem newItem = new MenuItem("New");
    MenuItem cutItem = new MenuItem("Cut", new ImageView("menu/cut.gif"));
```

You construct a Menu object in the same way.

```
    Menu editMenu = new Menu("Edit");
```

Add menu items, separators, and submenus to a menu object by adding them to the list of items:

```
    editMenu.getItems().addAll(cutItem, copyItem, pasteItem);
```

Alternatively, you can provide the children when you construct the menu:

```
    Menu optionsMenu = new Menu("Options", new ImageView("menu/options.gif"),
        readOnlyItem, insertItem, overwriteItem);
```

If you don’t want a decoration, supply null as the second argument.

Add the top-level menus to a MenuBar, and add the menu bar to the root pane: