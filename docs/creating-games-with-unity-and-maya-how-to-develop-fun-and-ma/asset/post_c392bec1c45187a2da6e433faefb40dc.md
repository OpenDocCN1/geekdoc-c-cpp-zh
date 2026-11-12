
### Why?

Although in the game the fog will be a great thing, it really makes it hard to work in the scene. While building the terrain, turning off the fog will give us a clear view of the shape and textures being formed.

**Step 2:** Create a terrain. Use Terrain > Create Terrain. This will create a huge terrain object with the corner at 0,0 in world space (Figure 6.9).

![](img/0285f88bc840f313779e011725b623a5_144_0.png)

*FIGURE 6.9 Newly created terrain.*

### Tips and Tricks

Note that when a terrain is added, new things appear all over the place. First, there is the physical placement of the terrain in the scene visible in the Scene window, but a terrain object also appears in the Hierarchy panel. Additionally, there is now a new terrain object in the Project panel. All of these are interacted with in different ways, but be aware that they are all present now.

**Step 3:** Resize the terrain. Select the terrain instance in either the Scene window or the Hierarchy panel. Choose Terrain > Set Resolution. Change the Terrain Width and Terrain Length to 150. Change the Terrain Height to 35 (Figure 6.10). Press Set Resolution.

![](img/0285f88bc840f313779e011725b623a5_144_1.png)

*FIGURE 6.10 Setting terrain size via the Set Resolution drop-down menu. Note that the results of the changes made do not appear until after the Set Resolution button was pressed.*

### Tips and Tricks

Note that the screenshot in Figure 6.10 shows the already resized terrain; however, Unity draws the newly sized terrain only after the Set Resolution button is pressed.

### Why?

Why not just use the Scale tool? It doesn't work on terrains. Probably because of the parametric and procedural basis of terrains, the Scale and Rotate tools won't affect them. The Move tool will, but the only way to change the size of a terrain is via the Set Resolution drop-down menu.

### Why?

Why so small? Remember that with the fog the player won't be able to see much beyond a few feet off the end of the dock. If a sunny bright scene was called for in the game, a big terrain could be great to show the other side of a river or bay and the land that emerges there, but in this case we are only building small chunks of stuff right around the existing geometry of the EntryWay. Keeping the terrain a reasonable size keeps all the relevant assets in a size and placement that makes moving around the scene easier.

A size of 150x150 is just an approximation of the size of the scene, and was found through trial and error. The height setting of 35 indicates the highest the mountains will rise off the surface of the terrain. This too can and might be edited later, but a reasonable height setting allows for easier fine-tuning as the terrain is painted.

**Step 4:** Move the terrain so that it sits beneath the water and extends beyond the edges of the dock, and also that the EntryWay is situated roughly in the middle of the terrain (Figure 6.11).

*FIGURE 6.11 Positioned terrain.*

![](img/0285f88bc840f313779e011725b623a5_145_0.png)

### Why?

Although terrains can be painted by raising parts up or pushing them down, I find it easiest to simply pull stuff up for the rough cut. And since the player should look down and see the water and not the mountain, sticking it below the water to begin with makes for a quick solution.

### Tips and Tricks

Remember the keyboard shortcuts for Move, Rotate, and Scale are the same in Unity as they are in Maya (W-Move, E-Rotate, R-Scale). Additionally, remember that the movement can be constrained with the cone handles on the manipulator once the Move tool is active.

**Step 5:** Examine the Inspector for the terrain:

## Terrain Editing Tools

Figure 6.12 shows the Inspector when the terrain is selected. At the top, there is the usual Transform component (although the Rotation and Scale settings here have no effect). On the bottom is the Terrain Collider component that allows the player to walk across the terrain. Right in the middle under the Terrain (Script) section are the tools that allow for the manipulation of the actual terrain.

These tools (Raise/Lower Terrain, Paint Height, Smooth Height, Paint Texture, Place Trees, Paint Details, Terrain Settings) allow for various modifications of the terrain. If the mouse hovers over any of the tool buttons a screen hint will pop up to indicate what the tool does. If a tool is selected, the options beneath it will change to allow for the specifics of how the tool works to be tweaked. Following is a brief description of what these tools do.

![](img/0285f88bc840f313779e011725b623a5_146_0.png)

*FIGURE 6.12 The Inspector for a terrain instance.*

- **Raise/Lower Terrain:** This works much like the Airbrush tool in Photoshop. A brush is defined by size and opacity (the rate the brush actually changes the area it is painting). Note that there are a bunch of different types of brushes (why anyone would use a Star brush is a mystery to me), but they can quickly all use organic forms as the brush is left in one spot or dragged across the surface. Clicking and holding or clicking and dragging raises the terrain surface until it reaches the Terrain Height setting defined in the Terrain Resolution from step 3, at which point the terrain will plateau. Holding the Shift button down while clicking and holding or clicking and dragging pushes the surface back down until it reaches its default starting height.

- **Paint Height:** In many ways this is similar to the Raise/Lower Terrain; however, it also allows for areas of the terrain to paint up to a specific height and stop (think tiered plateaus). To use it, either set the height with the slider, or Shift-click the terrain to define a target height, and then paint on the terrain to raise (or lower) the terrain to plateau at that target height.

- **Smooth Height:** Think of this as erosion. It smooths areas of the terrain and softens the area.

- **Paint Texture:** This tool allows the user to define textures and then apply them to the terrain. Note that this tool is useless until the tool has been told which textures can be used in the scene. This happens with the Edit Textures… button contained in the tool nested within the Inspector panel (much more on how to use this later). The power of this tool becomes apparent when there are several textures defined, and these textures are layered using various opacities upon the terrain.

- **Place Trees:** Much like the Paint Texture this allows for trees (as in geometry) to be placed on the terrain using a painting paradigm (or Paint Effects if you’re familiar with Maya). This tool does not include a wide variety of brushes, but the size of the default round brush can be changed as well as other variables including the density of trees as they are placed; the color, height, and width of the trees; and the variation of these attributes. Again, this tool is useless until tree meshes have been defined; this tool is done via the Edit Trees… button within the tool (nested in the Inspector panel). This tool can also be used to remove trees by Shift-painting over the terrain to remove all types of trees and Ctrl-painting to remove only the active types of trees.

- **Paint Details:** “Details” is kind of a funny word here. It actually means grass or detail meshes. Grass is an appealing part of Terrain as it is low poly but moves in the wind in believable ways and can really bring a scene to life. Detail meshes are things like rocks—things that when spread about on the scene and slightly adjusted in size or rotation can suddenly change the profile of the scene. Detail meshes can be anything really, including low vegetation. As expected, the tool only works after Grass or Detail Meshes have been defined. They are defined with the Edit Details… button in the Inspector when the Paint Details tool is active.

- **Terrain Settings:** This area includes a lot of settings that define how the terrain will react with the player. How far away from the player will a tree swap from a billboard to a high-poly tree? How hard and fast will the wind blow? How much will the wind bend elements? This and more await the user within the Terrain Settings. If there is a setting that should be adjusted for how the terrain looks or plays, chances are it's within this panel of sliders.

But enough of the grocery list of descriptions. Let's build something with it.

### Creating the Ground Topography

**Step 6:** Using the Raise/Lower Terrain tool, make a first rough pass similar to Figure 6.13. Don't worry about poking in too far into the dock, just use as big a brush as you can; just make sure it has a soft edge, and give the terrain a rough outline to mask out the edges of the dock and come up to the walls of the dock.

![](img/0285f88bc840f313779e011725b623a5_148_0.png)

### Tips and Tricks

Notice that generally the first pass here is simply a ridge of mountains around the outer ring of the shape of the EntryWay object. Big strokes like this are made to just give a little bit of structure to deciding what is needed. The key to effective terrain creation is multiple passes. Don't worry about getting any one area just right on the first pass.

**Step 7:** Add some mass to the terrain with further raising of the terrain (Figure 6.14). Again, use a large brush to quickly rough it out.

![](img/0285f88bc840f313779e011725b623a5_148_1.png)
