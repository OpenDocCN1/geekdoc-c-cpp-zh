# Chapter 24: Building Complex Scenes with Containers and XRefs

# Specifying an XRef as an overlay

The Overlay option in the XRef Scenes dialog box makes the XRef visible to the current scene, but not to any other scenes that XRef the scene including the overlay. This provides a way to hide XRef content from more than one level. Overlay XRefs also make it possible to avoid circular dependencies. For example, in previous Max versions, Max wouldn’t allow two designers to XRef one another’s scenes, but if one of the scenes is an overlay, this can be done.

# Working with XRef scenes

You can’t edit XRef scenes in the current scene. Their objects are not visible in the Select by Name dialog box or in the Track and Schematic Views. You also cannot access the Modifier Stack of external scenes’ objects. However, you can make use of external scene objects in other ways. For example, you can change a viewport to show the view from any camera or light in the external scene. External scene objects are included in the Summary Info dialog box.

# Tip

Another way to use XRef scenes is to create a scene with lights and/or cameras positioned at regular intervals around the scene. You can then use the XRef Scenes dialog box to turn these lights on and off or to select from a number of different views without creating new cameras. ■

You can also nest XRef scenes within each other, so you can have one XRef scene for the distant mountains that includes another XRef scene for a car.

# Note

If a Max file is loaded with XRef files that cannot be located, a warning dialog box appears, enabling you to browse to the file’s new location. If you click OK or Cancel, the scene still loads, but the external scenes are missing. ■

# Tutorial: Adding an XRef scene

As an example of a project that would benefit from XRefs, I’ve created a maze environment. I open a new Max file and animate a simple mouse moving through this maze that is opened as an XRef scene.

To set up an XRef scene, follow these steps:

+   1. Create a new Max file by choosing Application Button ➜ New.
+   2. Choose Application Button ➜ References ➜ XRef Scenes to open the XRef Scenes dialog box.
+   3. Click the Add button, locate the Maze.max file from the Chap 24 directory on the DVD, and click Open to add it to the XRef Scene dialog box list, but don’t close the dialog box just yet.

# Tip

You can add several XRef scenes by clicking the Add button again. You can also add a scene to the XRef Scene dialog box by dragging a .max file from Windows Explorer or from the Asset Manager window. ■

+   4. Select Create ➜ Helpers ➜ Dummy, and drag in the Perspective viewport to create a new Dummy object.
+   5. In the XRef Scenes dialog box, click the Bind button and select the dummy object. This enables you to reposition the XRef scene as needed.
+   6. Select the Automatic update option, and then click Close to exit the XRef Scene dialog box.
+   7. Now animate objects moving through the maze.