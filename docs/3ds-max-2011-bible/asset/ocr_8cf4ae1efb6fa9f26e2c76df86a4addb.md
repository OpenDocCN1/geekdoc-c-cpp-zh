# Part IV: Materials, Cameras, and Lighting Basics

# The Coordinates rollout

Every map that is applied to an object needs to have mapping coordinates that define how the map lines up with the object. For example, with the soup can label example mentioned earlier, you probably would want to align the top edge of the label with the top edge of the can, but you could position the top edge of the map at the middle of the can. Mapping coordinates define where the map’s upper-right corner is located on the object.

All map coordinates are based on a UVW coordinate system that equates to the familiar XYZ coordinate system, except that it is named uniquely so as not to be confused with transformation coordinates. For UVW coordinates, U represents the horizontal coordinate, V is the vertical coordinate, and W is along the surface normal. To keep them straight, remember that the UVW coordinate system applies to surfaces and that the XYZ coordinate system applies to spatial objects. These coordinates are required for every object to which a map is applied. In most cases, you can generate these coordinates automatically when you create an object by selecting the Generate Mapping Coordinates option in the object’s Parameter rollout.

# Note

**Editable meshes don’t have any default mapping coordinates, but you can generate mapping coordinates using the UVW Map modifier.**

In the Coordinates rollout for 2D Maps, shown in Figure 17.4, you can specify whether the map will be a texture map or an environment map. The Texture option applies the map to the surface of an object as a texture. This texture moves with the object as the object moves. The Environ option creates an environment map. Environment maps are locked to the world and not to an object. This causes the texture to change as the object is moved. Moving an object with an environment map applied to it scrolls the map across the surface of the object.

![](bbox=[0.086, 0.609, 0.419, 0.756])

Different mapping types are available for both the Texture and Environ options. Mapping types for the Texture option include Explicit Map Channel, Vertex Color Channel, Planar from Object XYZ, and Planar from World XYZ. The Explicit Map Channel option is the default. It applies the map using the designated Map Channel. The Vertex Color Channel uses specified vertex colors as its channel. The two planar mapping types place the map in a plane based on the Local or World coordinate systems.

The Environ option includes Spherical Environment, Cylindrical Environment, Shrink-Wrap Environment, and Screen mapping types. The Spherical Environment mapping type is applied as if the entire scene were contained within a giant sphere. The same applies for the Cylindrical Environment mapping type, except