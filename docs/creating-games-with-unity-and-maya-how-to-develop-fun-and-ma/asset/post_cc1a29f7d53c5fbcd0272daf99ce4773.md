
**FIGURE 5.15** Problem area found in a scene once placed in Unity

![](img/0285f88bc840f313779e011725b623a5_133_0.png)

> **Warnings and Pitfalls**
>
> In this case the problem was in my construction technique. As I was creating the doors, I duplicated a door and then scaled it using X = -1. The tricky thing about this is that in Maya, the normals look correct but in Unity they do not. The problem here is that by using the Scale X = -1 method, that mesh ends up with an Opposite tag that can be tough to track down. A better method is to use Mesh > Mirror Geometry when needing this sort of duplication.
>
> To fix this problem, either reconstruct using the Mirror Geometry method (and then separating the duplicate from the original (Polygons > Mesh > Separate)) or, take the errant copy and combine it with the original. Then the normals will appear as they will in Unity. Reverse the normals that are reversed (Polygons > Normals > Reverse), and separate the two doors. Be sure to rename the newly separated meshes appropriately.

- **Step 22:** In Maya, open the Maya file EntryWay.mb (**not** the .fbx we exported). Fix any geometry or normals problems.
- **Step 23:** Export manually from Maya again (File > Export All), although this time turn off Embedded Media in the File Type Specific Options section of the Export All dialog box. Be sure to overwrite the old EntryWay.fbx in the Assets folder of your Unity project file.

> **Why?**
>
> Because all the textures have already been imported into Unity, there is no need to include them in this new version of the .fbx. It will save loads of time in exporting and even more importing. By overwriting the old EntryWay.fbx, the changes made here will automatically fix themselves in the instances placed in the scene.

## Conclusion

So there it is—exporting manually from Maya and importing to Unity. I haven't had a project yet where I didn't have to do a little bit of tweaking to a level once it was imported. But because the process is so quick, it really is quite painless to make the necessary adjustments.

Now the game is playable enough to walk around the scene. It still has a lot of problems (no lighting, the sky is that strange flat blue, etc.), but not to fear; in the next chapters, we will use some of Unity's built-in asset creation tools to give more life to the scene.

## Homework and Challenges

- **Challenge 1:** If you've been building the hallway (along with UV and texture), export the hallway from Maya and create a new scene within Unity to place it in (save the file as Scene-Hallway). Walk through the level to test.

![](img/0285f88bc840f313779e011725b623a5_134_0.png)

## Asset Creation: Unity Scenography Creation Tools

### Asset Creation in Unity

In the previous chapters we have looked at using Maya as the primary asset creation tool. Indeed through the course of those tutorials we molded polygons and textured them using a tool completely outside of Unity.

Generally, this is how games are created: the assets are assembled in a package built for 3D object manipulation. Unity is just not a modeler (although it has been becoming an increasingly robust animator), and so to get complex forms and textures to bring those forms alive the game artist needs another package.

However, despite these limitations, Unity does have some asset creation capabilities. It can do more than simply bring assets in from outside. In this chapter, the EntryWay scene that has been created thus far will be further augmented with some of Unity's asset creation tools: built-in prefabs like water, terrains, trees, and particles.

## Tutorial 6.1: Adding and Manipulating Unity Water, Sky, and Fog

Before getting to the business at hand, it's worthwhile to revisit the idea of Packages. In Unity, we have seen how to import meshes that become GameObjects that have scripts attached to them and other components. These GameObjects can also have scripts and other functionality hung on them as additional components. When a GameObject has scripts attached to it, or special shaders to define the visual appearance, it can be a fairly robust asset.

To move these robust assets from project to project, Unity has developed this idea of packages that contain decorated and configured GameObjects. When the project was created, we imported the Character Controller packages that included the prefab GameObject of First Person Controller (which has already been used in the scene). At the time the project was created we refrained from adding other packages to keep the project lean and mean.

At this point, however, there are some very sophisticated and beautiful-looking prefabs that Unity has created that would be useful to us here ... specifically the water. In this tutorial we will look at importing these additional assets via packages and place them in our scene.

### Importing Packages

- **Step 1:** Open Unity. Make sure to set the project to Incursion—Unity.
- **Step 2:** Import Water packages. Choose Assets > Import Package > Water (Basic or Pro depending on which license you have). If you have Unity Pro, import the **Water (Pro Only)** package. If you are using the free Unity, use **Water (Basic)**.

> **Why?**
>
> What's the difference? Unity Pro includes some render to texture effects that allow for some very visually sophisticated water. Although you can import both packages (which I do for screenshot purposes here), if you do not have a Pro license, the functionality of the Pro water will not be seen.

- **Step 3:** After Unity decompresses the package, press Import in the Importing Package window that will pop up. Unity will then bring up an Importing Assets progress bar. When done, a new Water (Pro Only) folder or Water (Basic) folder will appear as a child of the Standard Assets folder within the Project panel.

### Water

- **Step 4:** Explore the water prefabs this process has brought in. In the Project panel, expand the Water folder and click once on one of the prefabs that has been imported (either Daylight Water/Nighttime Water or Daylight Simple Water/Nighttime Simple Water). The Inspector will explode with information. Notice that the GameObject will have some familiar components (Transform, Mesh Filter, Mesh Renderer) but will also contain a Water (Script) component and a very complex shader with lots and lots of inputs (especially if using the Pro version). This is the benefit of bringing in a package—all the appropriate textures that make the water look and move like water have been attached to the shader where they belong, and the script that further helps the effect has been attached and configured (Figure 6.1).

![](img/0285f88bc840f313779e011725b623a5_136_0.png)

**FIGURE 6.1** The settings of the Daylight Water prefab as brought in via the Water package.

- **Step 5:** Place the water in the scene. From the Project panel, drag one of the Daylight waters into the scene view (Figure 6.2).

> **Why?**
>
> Yes, the water could have been placed by dragging from the Project panel to the Hierarchy panel. However, by dragging directly into the scene, the water can be roughly positioned within the space. The results, however, are the same as dragging to the Hierarchy panel.

- **Step 6:** Move and scale the water to approximate Figure 6.3. The idea here is to make the water big enough so the edge cannot be seen inside the tunnel, and expands out past the edges of the dock enough so the edge is not too pronounced (we will hide it later with fog).

**FIGURE 6.2** Placing a water prefab by dragging from Project panel to the Scene view. Note that this is using the Pro version of water (real-time reflection).

![](img/0285f88bc840f313779e011725b623a5_137_0.png)

**FIGURE 6.3** Placed water.

![](img/0285f88bc840f313779e011725b623a5_137_1.png)

- **Step 7:** Play the game to check out the new water. Press the Play button (or press Ctrl-P on the PC or Command-P on the Mac) and walk around the scene to see how the water looks.

> **Why?**
>
> Don't worry too much about how this looks quite yet. It's very likely that in the game view the water looks way too blue (even if you are using a Pro license). This is because the water is reflecting the sky, which at this point is just a flat blue. It will be prettier as we define the environment further.

### Skyboxes

Skyboxes are interesting things. In effect they paint a sky behind everything in your scene. The sky behaves visually as the real sky does (although generally not animated). There are a few things that are a little unintuitive about them though. First, a skybox is not a GameObject—it can't be seen in the Hierarchy panel. Skybox materials are chosen in the Render Settings (of all places), and then Cameras have the option of whether to draw them or not. Second, skyboxes don't affect any sort of lighting or baking. They are images that look
