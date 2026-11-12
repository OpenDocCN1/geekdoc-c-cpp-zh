![](bbox=[0.136, 0.106, 0.638, 0.314])

FIGURE 12.1 Interface with GUI textures.

You can make these yourself if you’d like, or they can be downloaded on the supporting web site (http://www.Creating3dGames.com) as 2DAssets.unitypackage and imported into your project via Assets>Import Package>Custom Package.

A few notes about these textures for use in GUITextures:

+   - They were created in Photoshop.
+   - The size of the textures are all power of two. The buttons are 512×128, the logo is 1024×256, the data panels are 512×512, and the loading plate is 1024×1024. Although not strictly necessary, coming in as power-of-two textures makes the compression faster and keeps the images cleaner.
+   - Each of the textures (except for the Loading plate) have a distinct Alpha channel (not just a transparent background in Photoshop).

+   - **Step 1:** Make sure the assets are present in the project. They should be visible in the Project panel. If you imported the 2DAssets.unitypackage, they will be within a folder called 2D Assets.
+   - **Step 2:** Open the Unity scene Scene-Opening by double-clicking it in the Project panel. Remember that this is the scene we created earlier with Aegis spinning.
+   - **Step 3:** Organize the interface to allow the Game window to be clear and large. If you have a dual-monitor setup, setting up the Game window to fill an entire monitor is very helpful. Even if you don’t optimize by grabbing the Game tab and tearing it away from the Interface so that it is a floating window, resize the window to fill much of your available screen.

> > **Warnings and Pitfalls**
> > Remember that when bringing packages in, always use Assets>Import Package—dragging a package into your Assets folder will not work.

> > **Warnings and Pitfalls**
> > When this 2DAssets package is imported, you are likely to get some errors in relation to an "Unknown identifier: iTween". This is due to some things that we’ll work on later, so for now, don’t worry about these errors. They’ll be fixed later when iTween is brought into your project.

# ### Why?

Laying out GUI requires that the game can be seen. Making sure it’s not nested or squished within the Unity interface will provide a better chance of getting the look of the final game upon construction.