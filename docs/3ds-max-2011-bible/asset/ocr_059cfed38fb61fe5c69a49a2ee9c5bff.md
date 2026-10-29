# Part II: Working with Objects

You can now switch between the layers, depending on which one you want to add objects to or work on, and you can change properties as needed. For example, to focus on the deer object, you can quickly hide the other layers using the Layer Manager.

# Using the Scene Explorer

The Scene Explorer is a one-stop shop for all scene objects and display properties. It displays all the objects in the scene in a hierarchical list along with various display properties. It allows you to filter the display so you can see just what you want and customize the display so only those properties you want to see are visible. The Scene Explorer also lets you select, rename, hide, sort, freeze, link, and delete objects and change the object color.

A Scene Explorer dialog box, shown in Figure 6.19, is opened using the Tools↔ New Scene Explorer menu command (Alt+Ctrl+O). Each subsequent Scene Explorer view is numbered, but these individual views also can be named using the View field at the top of each Scene Explorer window. Each new or named view can be recalled with the Tools↔ Saved Scene Explorers menu, and the Tools↔ Manage Scene Explorers opens a simple dialog box where you can Load, Save, Delete, and Rename the saved views.

# Note

Scene Explorer views are automatically saved and reloaded with the Max file.

All scene objects in the Scene Explorer are listed in hierarchical order with children objects indented under their parent objects. You can expand or contract children objects by clicking the plus (+) or minus (–) icon to the left of the parent object.

# Selecting and filtering objects

If you click an object in the Scene Explorer dialog box, the object row is highlighted. Holding down the Ctrl key lets you click to select multiple objects, or you can use the Shift key to select a range of adjacent objects. Selected objects also can be removed from the current selection with the Ctrl key held down.

The Select menu also includes options for selecting objects. The All (Ctrl+A), None (Ctrl+D), and Invert (Ctrl+I) menu commands work as expected, selecting all objects, deselecting all objects, and selecting the inverse of the current selection. You also can access these commands using the buttons at the bottom of the dialog box.

The Select Children (Ctrl+C) option causes all children objects to automatically be selected when the parent is selected. The Select Influences option selects all influence objects that are attached to the selected objects. An influence object is an object that controls or shapes another object. For example, when a sphere is constrained to follow an animation path, the path is an influence object to the sphere. Another example is a skin mesh being influenced by a biped rig. The Select Dependencies option selects any objects that are dependent on the selected object, such as an instance and reference.

When the Select↔ Sync Selection option is enabled, any objects selected in the Scene Explorer dialog box are automatically selected in the viewports also. This also works in reverse, causing any objects selected in the viewport to be selected in the Scene Explorer dialog box.

The Scene Explorer recognizes any defined Selection Sets and lets you select these sets from the drop-down list at the bottom of the interface.