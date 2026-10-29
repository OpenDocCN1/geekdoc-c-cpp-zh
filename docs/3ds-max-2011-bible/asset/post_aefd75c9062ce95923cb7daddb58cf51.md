
# Working with the Schematic View

A valuable tool for selecting, linking, and organizing scene objects is the Schematic View window. This window offers a bird’s-eye view of the objects in your scene. From this whole scene perspective, you can find the exact item you seek.

The Schematic View window shows all objects as simple nodes and uses arrows to show relationships between objects. This structure makes the Schematic View window the easiest place to establish links and to wire parameters. You can also use this view to quickly see all the instances of an object.

## Using the Schematic View Window

A great way to organize and select objects is by using the Schematic View window. Every object in the Schematic View is displayed as a labeled rectangular box. These boxes, or nodes, are connected to show the relationships among them. You can rearrange them and save the customized views for later access.

You access the Schematic View window via the Graph Editors menu command or by clicking its button on the main toolbar. When the window opens, it floats on top of the Max interface and can be moved by dragging its title bar. You can also resize the window by dragging on its borders. The window is modeless and lets you access the viewports and buttons in the interface beneath it.

## The Graph Editors menu options

The Schematic View menu options enable you to manage several different views. The Graph Editors → New Schematic View command opens the Schematic View window, shown in Figure 25.1. If you enter a name in the View Name field at the top of the window, you can name and save the current view. This name then appears in the Graph Editors → Saved Schematic Views submenu and also in the title bar when the saved view is open.

Every time the Graph Editors → New Schematic View menu command is used, a new view name is created and another view is added to the Saved Schematic Views submenu. The Schematic View → Delete Schematic View command opens a dialog box in which you can select the view you want to delete.

### In This Chapter

- Working with the Schematic View window
- Working with hierarchies
- Setting Schematic View preferences
- Using List Views

> **Tip:** You can open any saved Schematic View window (or a new Schematic View window) within a viewport by right-clicking the viewport title, choosing Views → Schematic, and clicking the view name in the pop-up menu.

**FIGURE 25.1** The Schematic View window displays all objects as nodes.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_719_0.png)

## The Schematic View interface

The Schematic View window includes several common interface elements including menus, toolbar buttons, and a right-click quadmenu. Just like the main interface, you can access the commands in many ways.

### Using the Schematic View menus

The Schematic View window includes menus at the top of its interface, including Edit, Select, List Views, Layout, Options, Display, and View.

The Edit menu includes commands to Connect (C) and Unlink Selected object nodes. It also includes a Delete command, which deletes an object from the viewports as well as from the object node. The Edit menu includes commands to Assign Controllers, Wire Parameters, and a command to open the Object Properties dialog box.

> **Note:** Many of the keyboard shortcuts for the Schematic View window are the same as those in the main interface. If you enable the Keyboard Shortcut Override Toggle, then you can use the Schematic View keyboard shortcuts.

The Select menu includes commands for accessing the Select tool (S or Q); selecting All (Ctrl+A), None (Ctrl+D), and Invert (Ctrl+I); selecting (Ctrl+C) and deselecting children; and commands to sync the selected nodes in the Schematic View with the scene (Select From Scene) and vice versa (Select to Scene).

The List Views menu determines what is shown in the Schematic View. Options include All Relationships, Selected Relationships, All Instances, Selected Instances, Show Occurrences, and All Animated Controllers. Many of these options are also available in the Display Floater.

The Layout menu includes various options for controlling how the nodes are arranged. The Align submenu lets you align selected nodes to the Left, Right, Top, Bottom, Center Horizontal, or Center Vertical. You can also Arrange Children, or Arrange Selected. The Free Selected (Alt+S) and Free All (Alt+F) commands remove nodes from being auto arranged. With the Layout menu, you can also Shrink Selected, Unshrink Selected, Unshrink All, and Toggle Shrink (Ctrl+S).

The Options menu lets you select the Always Arrange option and view mode (either Hierarchy or Reference mode). You can also select the Move Children (Alt+C) option and open the Schematic View Preferences (P) dialog box.

The Display menu provides access to the Display Floater. The Display Floater (D) command opens the Display floater, which can be used to select the types of nodes to display. You also can hide and unhide nodes and expand or collapse the selected node.

The View menu includes commands for selecting the Pan (Ctrl+P), Zoom (Alt+Z), and Zoom Region (Ctrl+W) tools. You also can access the Zoom Extents (Alt+Ctrl+Z), Zoom Extents Selected (Z), and Pan to Selected commands. The View menu also includes options to Show/Hide Grid (G), Show/Hide Background, and Refresh View (Ctrl+U).

### Learning the toolbar buttons

You can also select most of these commands from the toolbar. Many of the toolbar buttons are toggle switches that enable and disable certain viewing modes. The background of these toggle buttons is highlighted yellow when selected. You’ll also find some buttons along the bottom of the window. All Schematic View icon buttons are shown in Table 25.1 and are described in the following sections.

> **Note:** The Schematic View toolbar buttons are permanently docked to the interface and cannot be removed.

**TABLE 25.1 Schematic View Toolbar Buttons**

| Toolbar Button | Name | Description |
|---|---|---|
| [icon] | Display Floater | Opens the Display Floater, where you can toggle which items are displayed or hidden. |
| [icon] | Select (S) | Toggles selection mode on, where nodes can be selected by clicking. |
| [icon] | Connect (C) | Enables you to create links between objects in the Schematic View window; also used to copy modifiers and materials between objects. |
| [icon] | Unlink Selected | Destroys the link between the selected object and its parent. |
| [icon] | Delete Objects | Deletes the selected object in both the Schematic View and in the viewports. |
|  | Hierarchy Mode | Displays all child objects indented under their parents. |
|  | References Mode | Displays all object references and instances. This mode displays all materials and modifiers associated with the objects. |
|  | Always Arrange | Causes all nodes to be automatically arranged in a hierarchy or in references mode, and disables moving of individual nodes. |
|  | Arrange Children | Automatically rearranges the children of the selected object nodes. |
|  | Arrange Selected | Automatically rearranges the selected object nodes. |
|  | Free All | Allows all objects to be freely moved without being automatically arranged. |
|  | Free Selected | Allows selected objects to be freely moved without being automatically arranged. |
|  | Move Children | Causes children to move along with their parent node. |
|  | Expand Selected | Reveals all nodes below the selected node. |
|  | Collapse Selected | Rolls up all nodes below the selected node. |
|  | Preferences | Opens the Schematic View Preferences dialog box. |
| My Saved View | View Name field | Allows you to name the current display. Named displays show up underneath the Graph Editors → Saved Schematic View submenu. |
| My Bookmark | Bookmark Name | Marks a selection of nodes to which you can return later. |
|  | Go to Bookmark | Zooms and pans to the selected bookmarked objects. |
|  | Delete Bookmark | Removes the bookmark from the Bookmark selection list. |

As you navigate the Schematic View window, you can save specific views as bookmarks by typing an identifying name in the Bookmark drop-down list. To recall these views later, select them from the drop-down list and click the Go to Bookmark icon in the Schematic View toolbar. Bookmarks can be deleted with the Delete Bookmark button.

> **Note:** Most of the menu commands and toolbar buttons are available in a pop-up menu that you can access by right-clicking in the Schematic View window.
