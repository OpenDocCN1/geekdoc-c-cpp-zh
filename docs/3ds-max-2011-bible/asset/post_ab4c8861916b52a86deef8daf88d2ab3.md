
# FIGURE 6.2

The Filter Combinations dialog box enables you to create a custom selection filter.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_216_0.png)

## Select buttons

On the main toolbar are several buttons used to select objects, shown in Table 6.1. The Select Object button looks like the arrow cursor. The other three buttons select and transform objects. They are Select and Move (W), Select and Rotate (E), and Select and Scale (R). These commands also are available on the quad menu. The final selection button is the Select and Manipulate button. With this button, you can select and use special helpers such as sliders.

## TABLE 6.1

### Select Buttons

| Button | Description |
| --- | --- |
|  | Select Object (Q) |
|  | Select and Move (W) |
|  | Select and Rotate (E) |
|  | Select and Scale (R) |
|  | Select and Manipulate |

## Cross-Ref

See Chapter 7, “Transforming Objects, Pivoting, Aligning, and Snapping,” for more details on the Select and Transform buttons.

## Selecting with the Edit menu

The Edit menu includes several convenient selection commands. The Edit ▸ Select All (Ctrl+A) menu command does just what you would think it does: It selects all unfrozen and unhidden objects in the current scene of the type defined by the selection filter. The Edit ▸ Select None (Ctrl+D) menu command deselects all objects. You also can simulate this command by clicking in any viewport away from all objects. The Edit ▸ Select Invert (Ctrl+I) menu command selects all objects defined by the selection filter that are currently not selected and deselects all currently selected objects.

The Edit ▸ Select Similar (Ctrl+Q) command selects all objects that are similar to the current selection. If multiple objects are selected, the Select Similar command selects the objects that meet the criteria for being similar to each of the selected objects. Objects are similar if they meet one of the following criteria:

- Same object type such as lights, helpers, or Space Warps
- Same primitive object such as Sphere, Box, or Hedra
- Same modeling type such as Editable Spline, Editable Poly, or Editable Patch
- Imported objects from an AutoCAD DWG file that have the same style applied
- Same applied material
- Objects existing on the same layer

Figure 6.3 shows a treasure chest of Hedra gems created in Chapter 5. With a single object selected, choosing Edit ▸ Select Similar (Ctrl+Q) causes all Hedra primitive objects to be selected.

## Select by Name

Choosing Edit ▸ Select by ▸ Name opens the Select From Scene dialog box, which is a version of the Scene Explorer dialog box, except that you can’t change any parameters. Clicking the Select by Name button on the main toolbar, positioned to the right of the Select Object button, or pressing the keyboard shortcut, H, also opens this dialog box.

## Cross-Ref

The Scene Explorer dialog box is covered in detail later in this chapter.

You select objects by clicking their names in the list and then clicking OK, or by simply double-clicking a single item. To pick and choose several objects, hold down the Ctrl key while selecting. Holding down the Shift key selects a range of objects.

## Select by Layer

The Layer Manager lets you separate all scene objects into layers for easy selection. The Edit ▸ Select by ▸ Layer command opens a simple dialog box listing the defined layers and lets you select a layer. All objects in the selected layer are then selected. The Layer Manager is covered in detail later in this chapter.

# FIGURE 6.3

The Select Similar command selects all Hedra objects.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_218_0.png)

## Select by Color

Choosing Edit→Select by→Color lets you click a single object in any of the viewports. All objects with the same color as the one you selected are selected. Even if you already have an object of that color selected, you still must select an object of the desired color. Be aware that this is the object color, not the applied material color. This command, of course, does not work on any objects without an associated color, such as Space Warps.

## Select by Region

The Edit→Selection Region command lets you select from one of two different methods for selecting objects in the viewport using the mouse. First, make sure that you’re in select mode, and then click away from any of the objects and drag over the objects to select. The first method for selecting objects is Window Selection. This method selects all objects that are contained completely within the dragged outline. The Crossing Selection method selects any objects that are inside or overlapping the dragged outline. You also can access these two selection methods via the Window Selection buttons on the main toolbar—Window and Crossing, shown in Table 6.2.

## Part II: Working with Objects

### Tip

If you can’t decide whether to use the Crossing or Window selection method, you can select to use both. The General panel of the Preference Settings dialog box provides an option to enable Auto Window/Crossing by Direction. When this option is enabled, you can select a direction, and the Crossing selection method is used for all selections that move from that direction. The Window selection method is used for all selections that move from the opposite direction. For example, if you select Left to Right for the Crossing selection method, then moving from Left to Right uses the Crossing selection method, and selecting from Right to Left uses the Window selection method.

### TABLE 6.2

**Window Selection Buttons**

| Button | Description |
|---|---|
| [图标] | Window |
| [图标] | Crossing |

You also can change the shape of the selection outline. The Selection Region button on the main toolbar to the left of the Selection Filter drop-down list includes flyout buttons for Rectangular, Circular, Fence, Lasso, and Paint Selection Regions, shown in Table 6.3.

### TABLE 6.3

**Shape-Shifting Selection Region Buttons**

| Button | Description |
|---|---|
| [图标] | Rectangular |
| [图标] | Circular |
| [图标] | Fence |
| [图标] | Lasso |
| [图标] | Paint |

The Rectangular selection method lets you select objects by dragging a rectangular section (from corner to corner) over a viewport. The Circular selection method selects objects within a circle that grows from the center outward. The Fence method lets you draw a polygon-shaped selection area by clicking at each corner. Simply double-click to finish the fenced selection. The Lasso method lets you draw by freehand the selection area. The Paint method lets you choose objects by painting an area. All objects covered by the paint brush area are selected.

# FIGURE 6.4

The drill’s front is selected using the Rectangular, Circular, Fence, and Lasso selection methods.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_220_0.png)

## Selecting multiple objects

As you work with objects in Max, you’ll sometimes want to apply a modification or transform to several objects at once. You can select multiple objects in several ways. Using the Edit ▸ Select by ▸ Name command, the Select by Name main toolbar button, or by pressing the H key, you can open the Select From Scene dialog box. With the Select From Scene dialog box open, you can choose several objects from the list using the standard Ctrl and Shift keys. Holding down the Ctrl key selects or deselects multiple list items, but holding down the Shift key selects all consecutive list items between the first selected and the second selected items.

The Ctrl key also works when selecting objects in the viewport using one of the main toolbar Select buttons. You can tell whether you’re in select mode by looking for a button that’s highlighted yellow. If you hold down the Ctrl key and click an object, then the object is added to the current selection set. If you drag over multiple objects while holding down the Ctrl key, then all items in the dragged selection are added to the current selection set.

### New Feature

When selecting multiple items in previous versions of Max, holding down the Ctrl key toggled the selection of objects, but in 3ds Max 2011, the Ctrl key is used only to add items to the selection. The Alt key is used to remove items from the selection.

The Alt key deselects objects from the current selection set, which is opposite of what the Ctrl key does.

If you drag over several objects while holding down the Shift key, then the selection set is inverted. Each item that was selected is deselected, and vice versa.

Object hierarchies are established using the Link button on the main toolbar. You can select an entire hierarchy of objects by double-clicking its parent object. You also can select multiple objects within the hierarchy. When you double-click an object, any children of that object are also selected. When an object with a hierarchy is selected, the Page Up and Page Down keys select the next object up or down the hierarchy.

Another way to select multiple objects is by dragging within the viewport using the Window and Crossing Selection methods discussed previously in the “Select by Region” section.
