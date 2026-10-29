# Creating reactor Objects

In addition to collections, reactor also includes several default objects that react with the scene in unique defined ways. These objects can be created using the Animation ▸ reactor ▸ Create Object menu commands or by clicking its icon in the reactor toolbar and dragging in one of the viewports.

The default objects include Spring, Plane, Linear Dashpot, Angular Dashpot, Motor, Wind, Toy Car, Fracture, and Water, as listed in Table 43.3.

# TABLE 43.3

# reactor Objects

| Toolbar Button | Name | Description |
|---|---|---|
|  | Spring | Acts to bring connected child and parent objects closer together |
|  | Plane | Adds a solid plane object to the scene |
|  | Linear Dashpot | Acts to limit linear motion between connected child and parent objects |
|  | Angular Dashpot | Acts to limit angular motion between connected child and parent objects |
|  | Motor | Used to add angular force to the scene |
|  | Wind | Used to add linear force to the scene |
|  | Toy Car | Simulates a simple car with rotating wheels and linear motion |
|  | Fracture | Identifies objects that can be broken into pieces |
|  | Water | Adds water to the scene that conforms to concave surface |

The gizmos for these objects, like the collection gizmos, appear red when first created for most of these objects and then turn white when selected, and blue when connected, to a geometry object. Figure 43.6 shows the gizmo icons for each of these reactor objects.

Most of these objects need to be associated with an object to be included in reactor. For example, the Toy Car reactor object must be connected to a geometry object for its chassis and up to four geometry objects for its wheels. This is done by clicking on the respective buttons in the Properties rollout and selecting the geometry object in the viewport. For example, you can connect a Spring object to both a Child and a Parent object. Other reactor objects, like the Plane and Wind objects, do not need to be connected to an object to work.