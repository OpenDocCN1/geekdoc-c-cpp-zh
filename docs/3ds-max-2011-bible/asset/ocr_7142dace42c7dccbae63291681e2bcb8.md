# Chapter 32: Unwrapping UVs and Mapping Textures

| Buttons | Name | Description |
|---|---|---|
|  | Scale, Scale Horizontal, Scale Vertical | Scales the selected vertices when dragged. |
|  | Freeform Mode | Displays a gizmo that you can use to transform the subobject selection. |
|  | Mirror Horizontal, Mirror Vertical, Flip Horizontal, Flip Vertical | Mirrors or flips the selected vertices about the center of the selection. |
|  | Show Map | Toggles the display of the map in the dialog box. |
|  | Coordinates | Displays the vertices for the UV, UW, and WU axes. |
| MAP #1 (CELLULAR) | Pick Texture drop-down list | Displays a drop-down list of all the maps applied to this object. You can display new maps by using the Pick Texture option. |
|  | Absolute/Relative Toggle | Lets you enter U, V, and W values as absolute values or relative offsets. |
| U: V: W: | U, V, W values | Displays the coordinates of the selected vertex. You can use these values to move a vertex. |
|  | Lock Selected Vertices | Locks the selected vertices and prevents additional vertices from being selected. |
|  | Filter Selected Faces | Displays vertices for only the selected faces. |
| All IDs | All IDs drop-down list | Filters selected material IDs. |

The buttons in the lower-right corner of the Edit UVWs dialog box work just like the Viewport Navigation buttons described in earlier chapters, including buttons to snap to grid and snap to pixel. You also can navigate about the Edit UVW window using the scroll wheel to zoom in and out of the window and dragging the scroll wheel to pan the view.

Within the Pick Texture drop-down list is a Checker Pattern option. This option applies a checker map to the mesh without having to assign a material. The checker pattern makes easy work of looking for stretching on the model.

# Using the Options panel

Many of the commands found in the menus also can be found in the Options panel at the bottom of the interface. You can expand these controls by clicking the Options button, shown in Figure 32.4. Using these controls, you can enable Soft Selection with a specified Falloff value. The UV and XY options let you switch between texture coordinates and object coordinates for the falloff. The Edge Distance lets you specify the Soft Selection falloff in terms of the number of edges from the selection instead of a falloff value. You also can choose the falloff profile as Smooth, Linear, Slow Out, or Fast Out.