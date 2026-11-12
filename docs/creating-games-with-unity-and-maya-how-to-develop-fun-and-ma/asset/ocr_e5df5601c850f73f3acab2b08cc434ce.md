**Warnings and Pitfalls**

If the folder next to the Image Name input field is clicked and you are not taken to the sourcemages folder of your project, stop. It means the project is not set right, and if you start maneuvering through file trees to find the right file, you could break the project on any other machine than the machine you are working on. If you find yourself in another location than what you anticipate, stop, save the file, and go back and set your project (File>Set Project).

**Step 7:** Choose Checkerboard.psd to define the color attribute. After following the previous step, the Attribute Editor will change to display a file node with an **Image Name** input field. Click the folder icon next to that input field, and you should be taken to the sourceimages folder of the project. Double-click Checkerboard.psd.

**Step 8:** View the scene in **Textured** mode. Do this by pressing **6** on the keyboard. This will show the scene with any applied textures and should yield a strange result as seen in Figure 3.4.

![](bbox=[0.44, 0.28, 0.83, 0.65])

FIGURE 3.4 Base checkerboard texture applied and the strange current default UV map.

**Why?**

So what are we seeing here? Think way back to when we first began building this column; the shape we began with was a cube. The parts of the column that have texture are the original faces of that cube. The polygons we extruded off of that shape are gray; they have no UV coordinates, and thus have no location for the texture to be "pinned" to. Further, the texture that is applied to the main shaft of the column is stretched and not efficiently organized.

# ## Mapping Beginning with Automatic Mapping

**Why?**

The first way we are going to look at UV mapping is to start with **Automatic Mapping**. Generally, anytime software does something "automatically" be a little wary—this is no exception. However, Automatic