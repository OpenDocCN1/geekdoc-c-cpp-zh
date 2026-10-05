
# Unity Games by Tutorials

# Chapter 1: Hello Unity

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_37_0.png)

Keep things tidy, move Bobble Wars Marine texture from the Models folder to the Textures folder. Textures are the basis of Materials.

What are materials, do you ask? Materials provide your models with color and texture based upon lighting conditions. Materials are what we know as shaders that ultimately determine what appears on screen. Shaders are small programs written in a specific shader language which is far beyond the scope of this intro book. You can learn more about materials through Unity’s included documentation.

Switch back to the Models folder and select BobbleMarine-Body. The Inspector will now display information specific to that model, as well as a preview.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_37_1.png)

If you see no preview, then your window is closed. At the bottom of the Inspector, find a gray bar then drag it upwards with your mouse to expand the preview.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_38_0.png)

The Inspector allows you to make changes to the model's configuration, and it allows changes to any selected object's properties. Since objects can be vastly different from one another, the Inspector will change context based on the object selected.

# Installing Blender

At this point, you've imported the models and texture for the space marine. The models were in FBX format, and the texture was in .PSD format.

We supplied the space marine models to you in the .FBX format, as this is a popular format for artists to deliver assets. But there's another popular format you should understand how to use it as well: Blender files.

Unlike .FBX, Blender files contain the source model data. This means you can actually edit these files inside Blender, and the changes will immediately take effect in Unity, unlike an .FBX file.

With an .FBX, you'd need to export and re-import the model into Unity every time you changed it.

There is a small tradeoff for all this delicious functionality. For Unity to work with Blender files, you need Blender installed on your computer. Blender is free, and you'll be happy to know that you'll use it to make your own models in a few chapters.

Download and install Blender at the following URL: https://www.blender.org/download/

# Creative Freedom Starts Here

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_39_0.png)

**Note:** Blender evolves at a rapid pace, so the version you see on your desktop will probably be different than this screenshot.

After you install Blender, run the app and then quit. That's it — you can now use Blender files with Unity.

## Importing packages

Now that you've installed Blender, you can now import the rest of the assets.

The rest of the assets are combined into a single bundle called a **Unity package**. This is a common way that artists deliver assets for Unity, especially when they purchase them from the Unity store.

Let's try importing a package. Select **Assets\Import Package\Custom Package...**, navigate to your resources folder and select **BobbleheadWars.unitypackage**, then click **Open**.

You'll be presented with a list of assets included in that package, all of which are selected by default. Note that some of these are Blender files, but there are also other files like textures and sounds as well. Click the Import button to import them into Unity.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_40_0.png)

The import will add a bunch of additional assets to your project. If you get a warning, just dismiss it.

To keep things tidy, single-click the newly generated Materials folder (in the Models folder) and rename it to Models. Drag this new folder into the parent-level Materials folder.

# Adding models to the Scene view

At this point, you have imported everything into Unity. It's time to starting your game together, and you'll kick it off by adding your models to the Scene view.

The Scene view is where game creation happens. It's a 3D window wherein you'll place, move, scale and rotate objects.

First, make sure to select the Scene view tab. Then, in the Project Browser, select BobbleArena from the Models subfolder and drag it into the Scene view.

# Unity Games by Tutorials

# Chapter 1: Hello Unity

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_0.png)

Check out the arena in the Scene view:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_1.png)

Pretty cool, eh?
The Scene view gives you a way to navigate your game in 3D space:

- **Right-click and rotate your mouse** to look around.
- **Hold down the right mouse button** and use the **WASD keys** to actually move through the scene.
- Moving too slow? Hold down **Shift** key.
- **Scroll with your mouse wheel** to zoom.
- **Move your mouse** to pan.

# Unity Games by Tutorials

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_41_0.png)

# Unity Games by Tutorials

By default, the view displays everything in shaded mode. You can switch to other modes such as wireframes. Let's try this out. In the Scene tab, click the shaded dropdown and select Wireframe.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_42_0.png)

Switch the Scene view back to shaded. You'll notice a gizmo in the right hand corner. This means the Scene view is in perspective; objects that are closer to you appear larger than those that farther away.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_42_1.png)

# Unity Games by Tutorials

Clicking on the axis will change your perspective. For example, click the green axis the scene will look down from the y-axis. How’s it feel to be on top?

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_43_0.png)

Clicking the center box will switch the view into Isometric a.a., Orthographic mode. Essentially, objects are the same size regardless of your proximity.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_43_1.png)

To return to Perspective mode, simply click the center box. You'll learn more about Isometric mode in this book.

# Adding the hero

At this point, you have the arena set up, but it's missing the guest of honor!
To fix this, in the Project Browser, find and open the Models folder then drag **BobbleMarine-Body** into the Hierarchy view.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_44_0.png)

In Unity, games are organized by scenes. For now, you can think of a scene as a level. The Hierarchy view is a list of all objects that are currently present in the scene.

Note that your scene already contains several objects. At this point, it contains your arena, the space marine, and two default objects: The main camera and a directional light.

With the marine body still selected, **hover the mouse** over the Scene view and press the **F** key to zoom to the marine. This shortcut is useful when you have many objects in your scene and you need to quickly get to one of them.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_45_0.png)

Don't worry if your space marine isn't placed at this exact position. You'll fix that later.

You'll notice that an object is selected, an outline appears around that object. Unity occasionally changes the outline color for selected objects from version to version.

In Unity 2018, new projects have a red outline. This is due to the new default color space of the editor. The color space determines how the engine mixes colors. It also determines what devices and platforms that game can support. By default, the color space is set to Gamma but you can switch it to Linear for new PCs, mobile devices, and current consoles (PS4, Xbox One, and the Nintendo Switch).

For now, it's best to use the default color settings, but you can easily switch from red to orange. You can always change the color by selecting **Edit,Preferences** on Windows or **Command-**, on macOS. From the Preference window, select **Colors** and you'll see a list of all the colors that you can customize. To change the selection outline field.
