
What does the ability to design and save custom levels allow you to do now? Share them of course! Be sure to post your levels on the http://raywenderlich.com forums for your fellow game designers to download and try out. Let's see how challenging you can make them all, and, of course, we want to see your best times.

> Note: As long as you don't introduce any new prefabs when building the levels, they'll work for everyone else who's working on this game.

## Section IV: Blender

In this section, you'll learn how to use Blender — a free 3D modeling and animation tool — to create great-looking assets for your games.

Along the way, you will create a scorpion enemy from scratch: including modeling, texturing, and animating.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_414_0.png)

- Chapter 15, "Modelling with Blender"
- Chapter 16, "Texturing with Blender"
- Chapter 17, "Animating in Blender"

## Chapter 15: Modeling in Blender
By Mike Berg

Blender is a free 3D modeling and animation tool. It is widely used and actively supported, but many game developers are immediately daunted by its unique user interface. Blender is very powerful, though, and more than capable of fulfilling your 3D asset-creation needs — once you know the basics!

In this chapter, you'll learn the basics of modeling in Blender as you build this formidable enemy below:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_415_0.png)

### Getting started

Before you dive in, make sure you have a two-button mouse with a scrollwheel. You should be able to click down on the scrollwheel itself for a middle-click. You will need all of these buttons while using Blender.

### Download Blender

Go to the Blender website to download Blender for Windows, Mac or Linux:

https://www.blender.org/download/

### Setting some defaults

By default, Blender selects objects with the right-mouse button, and it performs actions with the left-mouse button. By keeping the selection of an item separated from the action, you are less likely to select and move an item by mistake.

This makes Blender very awkward to beginners, but you get used to it in time. That, you can still change it so the left-mouse both selects and acts on an object, as is common with almost every app on Earth.

Open the preferences by selecting **File > User Preferences**. Click the **Input** tab at the top, click the **Select With: Left** button. This changes your left-mouse button to be your primary selection tool.

Secondly, if you are using a laptop — or any keyboard without a number pad — select the **Emulate Numpad** checkbox. This allows you to change the 3D view using the top row of numbers on your keyboard.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_416_0.png)

Click the **Save User Settings** button at the bottom, then close the preferences window.

Blender efficiency relies heavily on keyboard commands. They are even designed to be primarily on the left side of the keyboard, so that you can keep your left hand on the keyboard and your right hand on the mouse (with apologies to lefties!). You will primarily use keyboard commands when possible.

> Note: This chapter presents the shortcuts for the Windows version of Blender. To see the shortcuts for your own platform, select **File > User Preferences** and click on the **Input** tab.

### Creating your first model

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_417_0.png)

When you first open Blender, there's a cube in your scene. You're going to start with the wheels of the scorpion, so you don't need the cube. The thin white border around an object shows that it is selected, delete it by pressing... the **Delete** key?

Nope, not in Blender! Remember, common keyboard commands are on the left side of the keyboard, and the Delete key is *miles* away on the right side of the keyboard.

Press **X** to delete. A confirmation will appear under your cursor. Click it to delete your object.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_417_1.png)

Note: Hotkeys in Blender are specific to the panel your cursor is currently over. If a hotkey doesn't work as expected, move your cursor over the 3D View in the middle of your screen and try again.

### Re-inventing a wheel

Start by creating a cylinder for the cursor. To create a new object, press Shift-A.

- 1. A pop-up appears under your cursor. Select Mesh ▸ Cylinder.
- 2. Before you do anything else, you'll have to change some settings. At the lower-left of your screen, set the Vertices to 20, and the Depth to 0.3.
- 3. You should now have a cylinder that looks like this:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_418_0.png)

Stand the wheel on edge by pressing R to rotate it. Blender immediately enters a rotation mode; moving your cursor rotates the object freely.

- 1. Have a look at the small axis indicator at the lower-left. You want to rotate the cylinder on the Y axis.
- 2. Press Y and your rotation snaps to the y axis (note the green line through your model, indicating this).
- 3. You can drag your cursor around to rotate it, but for precise rotation you simply type 90 and press Enter to complete the rotation.

Unity Games by Tutorials

Chapter 15: Modeling in Blender

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_419_0.png)

To recap: Rotating an object is as simple as quickly typing one command, R Y 90 Enter.

> Note: This also works for both moving (type G for Grab) and scaling (type S), where the first command is the type of translation (move, scale or rotate), the second is the axis, and the third is the distance, scale factor or angle.

### The view from here

Before you edit the wheel any further, change the view so that you only see the side of it. Here are the keyboard shortcuts for changing the 3D View:

- 1: Front view
- 3: Side view
- 7: Top view
- 5: Toggle perspective

Press 3 5 to get a side view, with perspective turned off.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_419_1.png)

### Edit mode

Now the real fun begins. Get ready to edit some polygons!

Blender has several modes; right now you'll cover Object mode and Edit mode. In Object mode, you position objects within your scene. In Edit mode, you edit the polygons of an object. Press Tab to toggle between these two modes.

raywenderlich.com

Unity Games by Tutorials

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_420_0.png)

> Note: It can be easy to forget which mode you are in; you might be trying to do something in Edit mode that can only be done in Object mode, and vice versa.

### Slice-n-dice with Knife tool

The Knife tool creates a new edge on a face, cutting it into two. Create some boards on the front of the wheel by cutting it into four faces:

- 1. Press K, click once on the top-middle vertex, then click on the bottom vertex and press Enter to complete the operation.
- 2. Repeat the process for the vertices shown here...
- 3. ... here.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_420_1.png)

### Mesh Select mode

While in Edit mode, sometimes you want to work just with points (vertices), sometimes with edges, and sometimes with faces. There are three options for working with these elements: Vertex Select, Edge Select and Face Select. Switch between them by pressing Ctrl-Tab or by using the toggle buttons at the bottom of the3D View.

Switch to Face Select:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_420_2.png)

Select the newly created faces by clicking one, then holding Shift and clicking the others. Selected faces are highlighted.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_421_0.png)

> Note: If you make a mistake with a selection, undo works the same for selections as any other action. You can also press A to toggle “select all” and “select none.”

### Orbiting the camera

You need a slightly different view of your model to see the next operation properly. Middle-click and drag to orbit the camera around your model.

> Shift + middle-click and drag to pan the view, and use your scroll wheel to zoom in and out.

Orbit around your wheel to get a view similar to this:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_421_1.png)

### The Inset tool

The Inset tool creates a smaller copy of the currently selected face.

- Press I to invoke the Inset tool. Drag the cursor toward the center of the object and the inset adjusts.
- You want each individual face to be inset, rather than the whole group of faces. Press I again to enter the tool's Individual mode.
