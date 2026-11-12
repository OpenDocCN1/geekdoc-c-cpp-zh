
## Tutorial 3.1: Game Level UV Layout, Tools, and Techniques

In this tutorial, we will continue working on the EntryWay we began earlier. Although we won't explicitly map every object, the techniques covered here are extensible to all the objects in this scene, and indeed into all the scenes in the rest of the game.

- **Step 1:** Create a checkered pattern. In Photoshop, create an image that is 32×32 pixels. Create guides horizontally and vertically in the middle of the canvas. Fill the top-left and bottom-right with black. Select all, choose Edit>Define Pattern. Name the pattern.

- **Step 2:** Create a checkered base texture. Create a new image that is 1024×1024. Choose Edit>Fill. In the Fill dialog box, choose Use:Pattern and pick the previously created checkered pattern and click OK. The results should look like Figure 3.3. Pretty exciting, eh?

![](img/0285f88bc840f313779e011725b623a5_61_0.png)

FIGURE 3.3 Base checkered texture.

### Why?

Why a checkered pattern? Why not just use the checkered texture that's canned in Maya? Why 1024×1024? All good questions. As we attempt to lay out the UV map, it will be important to know that the mapping we have created does not cause stretched or pinched textures. Further, sometimes we want to know how much texture is actually on any one part of the mesh. By using a checkered texture, we can have a quick reference of how the texture is mapped across the surface, and how we are distributing the texture in 3D space. The reason to build our own instead of using Maya is that the Maya checkerboard is set at the number of checks across and down. By creating our own, we can create a more densely populated collection of checks. The file is 1024×1024 because we want to get in the habit of building by **power of two** when working with texture (much more about this later).

- **Step 3:** Save as Checkerboard.psd in the sourceimages folder of the project file.

### Why?

The sourceimages folder is where Maya goes to look for textures when a new material is created. There are lots of other seductively logical folders (images, textures, etc.) but don't succumb. The only folder that matters for saving textures within Maya is sourceimages.

### Creating and Applying New Material

- **Step 4:** Create and apply a new material on a column. Right-click and hold on the column that we previously beveled. Choose Assign New Material. In the Assign New Material window, click Lambert. This should open a new lambert material in the Attributes Editor. If it does not, press Ctrl-A, and the Attribute Editor will show the attributes of this new material.

### Why?

Why a lambert? Lamberts are matte materials that Maya draws really quickly and well. More importantly for us, when Unity initially brings in the Maya-created objects, everything looks like a lambert. Any other attributes present in other materials (specular in Phong, etc.) has to be redefined in Unity anyway. So spending a lot of time tweaking settings in Maya is wasted since it has to be redone. For this reason, lamberts are quick, easy, and predictable ways to get textures applied and to see the general look of the scene.

- **Step 5:** Name the material. Name the material. Name the material. Did I mention to name the material? Name the material `EntryWay_Column_Mat`.

### Why?

Beginning modelers or beginning game builders often skip effective naming and pay the horrible price later. When moving assets between applications (like from Maya to Unity), assets will be tied together differently, and sometimes in the production process materials will become disconnected from objects. If there are 100 materials named lambertx, you will be immensely slowed in your work. Take just a little time to name materials what they are, and you will save many hours later. Especially if you ever hope to work with others as part of a team—effective naming is critical to smooth work flows and keeping your job.

- **Step 6:** Create a Render Node for the Color attribute. In the Attribute Editor, at the far right of the Color channel is a little button that (ironically) looks like a checkerboard. Click this to bring up the Create Render Node window. Tell Maya to import a file to define the color attribute of the material by clicking the File button.

### Warnings and Pitfalls

If the folder next to the Image Name input field is clicked and you are not taken to the sourceimages folder of your project, stop. It means the project is not set right, and if you start maneuvering through file trees to find the right file, you could break the project on any other machine than the machine you are working on. If you find yourself in another location than what you anticipate, stop, save the file, and go back and set your project (File>Set Project).

- **Step 7:** Choose Checkerboard.psd to define the color attribute. After following the previous step, the Attribute Editor will change to display a file node with an **Image Name** input field. Click the folder icon next to that input field, and you should be taken to the sourceimages folder of the project. Double-click Checkerboard.psd.

- **Step 8:** View the scene in **Textured** mode. Do this by pressing **6** on the keyboard. This will show the scene with any applied textures and should yield a strange result as seen in Figure 3.4.

![](img/0285f88bc840f313779e011725b623a5_63_0.png)

FIGURE 3.4 Base checkerboard texture applied and the strange current default UV map.

### Why?

So what are we seeing here? Think way back to when we first began building this column; the shape we began with was a cube. The parts of the column that have texture are the original faces of that cube. The polygons we extruded off of that shape are gray; they have no UV coordinates, and thus have no location for the texture to be "pinned" to. Further, the texture that is applied to the main shaft of the column is stretched and not efficiently organized.

### Mapping Beginning with Automatic Mapping

### Why?

The first way we are going to look at UV mapping is to start with **Automatic Mapping**. Generally, anytime software does something "automatically" be a little wary—this is no exception. However, Automatic Mapping does create UVs for all the geometry we have, and once we have those UVs we can fix the map into what we need.

- **Step 9:** Use Automatic Mapping on the column. With the column selected, choose Polygons>Create UVs>Automatic Mapping (Figure 3.5). In the UV Texture Editor window, choose Image>Display Image (to turn off the checkerboard), and see the shapes that represent the column.

![](img/0285f88bc840f313779e011725b623a5_64_0.png)

FIGURE 3.5 Results of Automatic Mapping.

### Why?

At first glance all is well—that was amazingly easy. But take a look at the UV Texture Editor (Window>UV Texture Editor) and you'll notice a couple of important things. In the UV Texture Editor window choose Image>Display Image (to turn the background checkerboard off), and see the shapes that represent the faces of the column. First, notice that there is a lot of the texture space that we are not making use of. In the game, we are paying for that space whether we use it or not, and it's very inefficient to leave so much of that texture space unused. Second, notice that each of the sides of the column are separate. This means that the texture won't crawl around the corners or the column—there will be a seam across every corner of our form.

Seams are inevitable. If a form is to be unwrapped, there has to be a seam somewhere, but we want to minimize those. To do this, we will be cutting up some of this map and reassembling (via sewing) other parts.

- **Step 10:** Cut the heads off the columns. In the UV Texture Editor, right-click and choose Edge from the hotbox. Select the edges (there are really three there, although they are all in a line) shown in Figure 3.6. In the Editor window choose Polygons>Cut UV Edges.

![](img/0285f88bc840f313779e011725b623a5_65_0.png)

### Why?

We are cutting the heads off so we can sew up the side edges of the shaft. In the game, we will see much more of the shaft than the capital of the columns. So making sure there is only one seam on the shaft makes for a better experience for the game player.

- **Step 11:** Move the head away via UVs. Right-click again and choose UV from the hotbox. Marquee select a few UVs (that are part of the column capital - maybe the top right corner of UVs) and then Ctrl-right-click-hold (I know it's a lot) and choose To Shell (Figure 3.7). This will select the shell of UVs that make up the top of the column. Move them aside. Moving a UV shell can be done with the regular Move tool (press W to activate it) or in the Editor window choose Tool>Move UV Shell Tool and then move them aside (anywhere really).

![](img/0285f88bc840f313779e011725b623a5_65_1.png)

### Why?

What is a shell? Shells of UVs are shared UVs that share UVs, or edges. Because we cut the edges at the bottom of the column capital, the edges there were no longer shared, so when we selected a shell, it stopped there.
