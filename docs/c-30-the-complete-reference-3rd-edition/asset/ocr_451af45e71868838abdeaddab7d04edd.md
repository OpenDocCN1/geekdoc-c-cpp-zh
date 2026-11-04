# Adding a Menu

The main window of nearly all Windows applications includes a menu across the top. This is called the main menu. The main menu typically contains top-level categories, such as File, Edit, and Tools. From the main menu descend drop-down menus, which contain the actual selections associated with the categories. When a menu item is selected, a message is generated. Therefore, to process a menu selection, your program will assign an event handler to each menu item. Because menus are such a bedrock resource in Windows programming, many options are available and the topic of menus is quite large. Fortunately, it is easy to create a simple main menu.

Originally, there was only one way to create a main menu: by using the classes MainMenu and MenuItem, both of which inherit the Menu class. These classes create the traditional-style menus that have been used in Windows applications for years. This approach is still supported. However, version 2.0 of the .NET Framework added a second way to add menus to a window by using a set of classes based on ToolStrip, such as MenuStrip and ToolStripMenuItem. Menus based on ToolStrip have many additional capabilities and give a modern look and feel. Understand, though, that both approaches to menus are currently valid for new C# applications.

Because there are two ways to create menus, both ways are described here, beginning with the traditional approach.

# Creating a Traditional-Style Main Menu

A traditional-style main menu is constructed from a combination of two classes. The first is MainMenu, which encapsulates the overall structure of the menu. The second is MenuItem, which encapsulates an individual selection. A menu selection can either represent a final action, such as Close, or activate another drop-down menu. As mentioned, both MainMenu and MenuItem inherit the Menu class.

When a menu item is selected, a Click event is generated. Click is defined by MenuItem. Therefore, to handle a menu selection, your program will add its handler to the Click event list for that item.

Each form has a Menu property, which is defined like this:

```
public MainMenu Menu { get; set; }
```

By default, no menu is assigned to this property. To display a main menu, this property must be set to the menu that you create.

Creating a main menu is straightforward, but it does involve several steps. Here is the approach we will use:

+   1. Create a MainMenu object.
+   2. To the MainMenu object, add MenuItems that describe the top-level categories. This is done by calling Add() on the collection referred to by the MenuItems property.
+   3. To each top-level MenuItem, add the list of MenuItems that defines the drop-down menu associated with that top-level entry. This is also done by calling Add() on the collection referred to by the MenuItems property.
+   4. Add the event handlers for each selection.
+   5. Assign the MainMenu object to the Menu property associated with the form.