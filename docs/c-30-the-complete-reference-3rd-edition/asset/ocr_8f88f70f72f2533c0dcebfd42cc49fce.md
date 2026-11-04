Finally, the MainMenu object must be assigned to the Menu property of the form, as shown here:

```
Menu = MyMenu;
```

After this assignment takes place, the menu will be displayed when the window is created, and selections will be sent to the proper handler.

The following program puts together all the pieces and demonstrates how to create a main menu and handle menu selections.

```
```csharp
// Add a Main Menu.
using System;
using System.Windows.Forms;

class MenuForm : Form {
    MainMenu MyMenu;
    public MenuForm() {
        Text = "Adding a Main Menu";
        // Create a main menu object.
        MyMenu = new MainMenu();
        // Add top-level menu items to the menu.
        MenuItem m1 = new MenuItem("File");
        MyMenu.MenuItems.Add(m1);
        MenuItem m2 = new MenuItem("Tools");
        MyMenu.MenuItems.Add(m2);
        // Create File submenu.
        MenuItem item1 = new MenuItem("Open");
        m1.MenuItems.Add(item1);
        MenuItem item2 = new MenuItem("Close");
        m1.MenuItems.Add(item2);
        MenuItem item3 = new MenuItem("Exit");
        m1.MenuItems.Add(item3);
        // Create Tools submenu.
        MenuItem item4 = new MenuItem("Coordinates");
        m2.MenuItems.Add(item4);
        MenuItem item5 = new MenuItem("Change Size");
        m2.MenuItems.Add(item5);
        MenuItem item6 = new MenuItem("Restore");
        m2.MenuItems.Add(item6);
        // Add event handlers for the menu items.
        item1.Click += MMOpenClick;
        item2.Click += MMCloseClick;
```
```