collection. Or you could click the Add button to open a Select Object dialog box where you can select objects from a list. The collection objects are then displayed in a list found in the Properties rollout. Clicking the highlight button in the Properties rollout briefly turns white all objects that are part of the collection.

# Caution

A single object can be added to multiple collections, but this causes a warning to appear when you try to preview the animation.

If an object is selected before you create a collection icon, then the selected object is automatically added to the collection, and the collection icon is positioned at the Pivot Point of the selected object or objects.

# Collection modifiers

If you tried several times to add an object to a Cloth collection with no luck, then this section is for you. Before you can add objects to the Cloth, Rope, or Soft Body collections, you need to apply the Cloth, Rope, or Soft Body modifiers to the object. To apply a modifier to an object, select the object in the viewport, choose Animation reactor Apply Modifier, and choose the modifier type to apply. Table 43.2 shows the three reactor modifiers.

# Note

The Rope modifier can be applied only to splines or shapes.

TABLE 43.2

reactor Modifiers

| Toolbar Button | Name | Description |
|---|---|---|
|  | Cloth Modifier | Allows objects to be simulated as cloth |
|  | Soft Body Modifier | Allows objects to be simulated as soft bodies |
|  | Rope Modifier | Allows objects to be simulated as rope |

Each of the reactor modifiers has a Vertex subobject mode available in the Modifier Stack. Selecting a vertex allows you to give it different physical properties from the rest of the vertices. For example, you could select the vertices at one end of a rope to have a higher Mass value where it connects with a hook. This end would then fall under gravity before the other end.

# Setting object properties

After collections have been added to the scene and objects have been added to the collection, you can define the physical properties using the Property Editor, shown in Figure 43.4. You can open the Property Editor by selecting Animation reactor Open Property Editor. To set the properties for the objects, you need to select the object and not the collection icon. The Property Editor lets you set the properties for many selected objects at the same time. The title bar of the Property Editor identifies the collection whose properties you are setting.