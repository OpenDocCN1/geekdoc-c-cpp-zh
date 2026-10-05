# Unity Games by Tutorials

+   2. Press Ctrl-M to invoke the Mirror tool. Nothing noticeable changes, but if you look at the bottom of the 3D View, you'll see that the menu bar has changed to a status bar, with the text Select a mirror axis (X, Y, Z).

+   3. Press X, then Enter to complete the Mirror operation.

![](bbox=[0.156, 0.248, 0.833, 0.375])

> Note: The status bar shows changes and options for more tools. It's a good thing to glance at while performing different tasks.

# # Changing the pivot point

Now, this is mirrored correctly, and you could move the object over, but there's a way to mirror and move it in one step. Press Ctrl-Z to undo the Mirror operation.

Blender operations are always centered around a pivot point. So far, have been using the default pivot point, which is the origin of the current object. There are several other options for the pivot point, which you can see in the menu at the bottom of the 3D View:

![](bbox=[0.303, 0.649, 0.696, 0.803])

Change the Pivot Point to 3D Cursor, which is at the center of the scene (remember, press Shift-S and select Cursor to Center if your cursor has been moved). Now when you mirror the arm, it will not only flip, but flip over the cursor.

Give it a try; press Ctrl-M X and Enter to mirror over the X-axis.