
For our uses we will be focusing primarily on polygonal modeling techniques (the techniques using the tools in Maya's Polygons mode). The other methods of NURBS (non-uniform rational b-splines) and Subdivs are too indirect in their creation of polygons, and thus we lose control over polygon placement and count.

### Topology

Topology refers to the structure or organization of polygons on a surface. Topology matters. Correctly structuring polygons makes a huge difference in how the mesh can be deformed later (with things like joints), how the form interprets collisions in Unity, and how easy it is to lay out UV maps. Much of topology concern centers around the tessellation process—the process of converting the form into three-sided polygons (tris) when it comes time to render.

Maya, like most 3D software, allows the user to create polygons of any number of sides (usually called n-gons). This is relatively new in the 3D production history. Not many years ago, 3D software would allow polygons to be constructed only as tris or quads (four-sided polygons). Tris are pretty hard to work with and manipulate quickly, so quads became the preferred method of organizing polygons. To allow artists to more fluidly create forms, most 3D apps began allowing the user to pay no attention to the number of sides of a polygon as the form was built. However, woe be the modeler who doesn't pay attention to the construction of his polygons. Five- (and more) sided polygons cause all sorts of problems down the road.

The issue is in the tessellation process. When the 3D software (or game engine, like Unity) converts a 3D form into all tris (which it must for the video cards to draw them), there are some shapes that are easier to tessellate. A quad is relatively easy, since it just splits it in half from vertex to vertex (Figure 2.4). However, the tessellation of the n-gon is often unpredictable, especially from a game asset creation standpoint. It does it for sure, but the resulting mesh is a mess (Figure 2.5).

This messy tessellation that can be seen in Figure 2.5 may not seem to be a big deal here, but when these polygons are subjected to distortion techniques (like bending a mesh with joints), suddenly the edges where things can actually bend end up being in unpredictable places and result in

![](img/0285f88bc840f313779e011725b623a5_36_0.png)

**FIGURE 2.4** Tessellating a quad is pretty straightforward. Just split it corner to corner to create two tris.

remaining parts of the level, you can simply use the versions that are included on the web site (http://www.Creating3dGames.com). However, if you’re looking to make sure your game modeling skills are tight, be sure to attempt the challenges at the end of the chapter and complete the entire level by yourself.

## Tutorial 2.1: Game Level Modeling: The Entryway

The entry of the Balaklava facility is a great place to start. First, the parts that make up the entry are largely rectilinear. Anything man-made and rectilinear is easily created in 3D applications. Second, all these rectilinear forms are a perfect trap for beginning modelers—a trap to create shapes that neither produce the appropriate sense of age or dirt. Over the course of the tutorials, we will look at taking a simple geometric space and making it look like it’s been around for a while (Figure 2.6).

- **Step 1:** Double-check you’ve got a project set up called “Incursion–Maya.” If you don’t, or don’t know how, check out Appendix A.
- **Step 2:** Choose File > Save Scene (Options).
- **Step 3:** Check Incremental Save and click Save Scene.

### Why?

Incremental Saves are insurance policies. What happens is that each time a scene is saved, Maya makes a copy of the scene from the last time it was saved and saves it to a folder called incrementalSave. This does mean that there are lots of copies of your file, but it makes sure that the catastrophic case of corrupted files, you have a backup. Even if you run out of “undos,” incrementalSaves folder means you can go back in time to what you wanted or needed. Every single semester I have taught, incremental saves have saved at least one student’s project.

**Step 4:** In File Name: enter `EntryWay` and click the Save button. Note that if the project has been defined correctly, you are in the Incursion–Maya\scenes folder.

> **Warnings and Pitfalls**
>
> I know it’s tempting to skip this step since you’re anxious to get started. Worse, I see lots of students who don’t quite understand this step and skip it because it doesn’t seem important. But keeping track of your assets is critical to success in projects as diverse as games. Create and Set your project in Maya. You must know that your texture files are in the sourceimages folder, and that your scene files are in your scenes folder.

![](img/0285f88bc840f313779e011725b623a5_38_0.png)

**FIGURE 2.6** Completed model at the end of this tutorial.

### Dock Creation

**Step 9:** Begin creation of the cement dock area in a similar fashion. Start with a cube (renamed in the Outliner to `EntryWayDock`) that is X = 20, Y = 4, Z = 60 (this can be adjusted later as we build), and extrude the faces as shown in Figure 2.10.

**FIGURE 2.10** Beginning to lay out dock.

![](img/0285f88bc840f313779e011725b623a5_41_0.png)

**Step 10:** Continue working around the dock making sure to make extrusions at locations that will allow for new extrusions that will allow for holes (Figure 2.11).

**FIGURE 2.11** Continuing dock layout.

![](img/0285f88bc840f313779e011725b623a5_41_1.png)

### Tips and Tricks

Deciding when to make extrusions is a skill you build up over time and with experience. I find that sketching out the shape I want to make on a sheet of paper, and then sketching out the places that extrusions would need to be made, helps me quite a bit when it comes time to do it digitally.

**Step 11:** Here's where things might get a bit tricky. What we want to do is make sure we have new locations to build outcroppings of the dock. Look carefully at how extrusions are made to allow for future extrusions that make the stepping out. Notice that this creates some pretty inefficient topology (geometry where there needn't be), but we will clean that up in a bit (Figure 2.12).

![](img/0285f88bc840f313779e011725b623a5_42_0.png)

### Tips and Tricks

This part of the process is really about roughing out the shape. It won't be perfect right away, so don't worry too much about being exact. When creating this tutorial, I ended up with lots and lots of undos to get back to a place that would allow me to more efficiently create the form. 3D creation is a process of stops and starts to be certain.

**Step 12:** Create a stepped section by deleting faces and filling them in with the Append to Polygon tool. Select the faces on the far corner (as shown in Figure 2.13) and delete them. This will leave a hole in the mesh that needs to be filled. One way to fill this is the Append to Polygon tool. To use this tool, be sure to be in Object Mode (right-click the object and select Polygon Tool) and click an edge of the hole. Purple arrows will appear that show the path of the new polygon that will be created. Click these arrows until the face is filled and press Enter. Repeat for the other plane that needs to be filled.

![](img/0285f88bc840f313779e011725b623a5_42_1.png)

### Tips and Tricks

When using the Append to Polygon tool, usually there is no need to go all around the outside of the shape that is being filled. It is faster to click one edge, and then click the edge opposite that edge and press Enter. This fills the hole quickly as it figures out the other edges are included in the function.

### Tips and Tricks

Notice that after filling the hole, there will be some black chunks across the new planes that have been made. This is happening because the new polygon has **soft normals**, which are great for organic shapes, but not so great with rigid forms like this dock. To get rid of these, select the object and choose Polygons>Normals>Harden Edge.

**Step 13:** Rotate the front of the dock. Right-click the dock and choose Vertex from the hotbox menu. Marquee select the vertices across the front of the dock as shown in Figure 2.14. Choose the Rotate tool (keyboard shortcut is the E key), and then (to move the axis of rotation) press and hold the D key on the keyboard. Move the manipulator handles back to the back corner of the collection of vertices that have been selected. Release the D key and rotate the vertices from this new axis just defined.

![](img/0285f88bc840f313779e011725b623a5_43_0.png)

**FIGURE 2.14** Rotating a collection of points from a new axis of rotation.

### Tips and Tricks

This rotation trick or moving the axis of rotation (via holding down the D key or by pressing the Insert key) works in Object mode too. The axis of rotation can be moved to wherever it needs to be for a given object. In our case, it's temporary for a selection of components (vertices in this example), but when done while in Object mode, the object will "remember" this new axis location.

### Dock Optimization

**Step 14:** Optimize the mesh. In the process of outlining this shape, we have quickly made some shapes that could be optimized. As pointed out earlier, polycount is rarely the problem with slow games, but it is certainly one of them. Especially if you are developing for iOS (iPad, iPhone, iPod Touch) or Android, keeping a tight grasp on polycount will be critical.
