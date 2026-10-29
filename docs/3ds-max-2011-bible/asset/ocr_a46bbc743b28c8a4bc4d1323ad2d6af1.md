Pelt mapping overcomes these difficulties by allowing the user to define the seams for the mesh. These seams can be located along material boundaries or along mesh borders. The vertices along these defined seams are then positioned around the edges of a circle called the Stretcher and pulled until the mesh UVs are pulled flat. This results in clearly displaying and flattening all the UVs for the selected part, allowing you to easily paint and apply a texture map.

Before you can start pulling the pelt tight, you need to define the seams that will be used to cut the model. These seams should be located in areas of the model that won’t be clearly visible. For example, if you are unwrapping a head model, the back and top of the head is a good choice because it probably will be covered with hair that will hide the seam. Locating a seam on the midline up the front of the face is a terrible choice, because lining up face details like the lips and the nose on opposite ends of the map is difficult.

# Selecting seams

The first step of pelt mapping is to select the seams for the map. To do this, click the Face subobject mode and then use the four buttons located in the Map Parameters rollout to define the pelt seams. These seams are displayed in light blue as they are created.

# Note

All open borders are automatically made into seams.

The Edit Seams button, at the bottom of the rollout, lets you click edges to highlight them as seams. This can be time consuming if you have a complex mesh. The Point to Point Seam button lets you click a starting point; a rubber band line then appears that lets you extend to an ending point. A seam is created between these two points using the shortest possible route. After an ending point is selected, the rubber band remains, letting you add to the seam. Right-click to exit the rubber band and to choose a new starting point. Figure 32.16 shows the seams added to the head model.

# Tip

When placing pelt mapping seams, try to position the seams where they aren’t readily visible, such as under the arms and legs or down the middle of the back.

The Edge Selection to Pelt Seams button converts an existing edge selection to a pelt seam, and the Expand Face Selection to Pelt Seams button selects all faces that are next to the pelt seams.

The Parameters rollout contains an option to Always Show Pelt Seam. If this option is enabled, then the pelt seam is clearly shown. You also can set the size of the seams to thin or thick.

# Positioning the projection gizmo

After the seams are defined, select all the faces that are to be mapped and click the Pelt button in the Map Parameters rollout. This opens the Edit UVW window along with the Pelt Map panel, shown in Figure 32.17.