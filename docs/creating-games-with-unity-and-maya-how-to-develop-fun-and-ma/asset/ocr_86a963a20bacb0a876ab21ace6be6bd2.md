**FIGURE 6.2** Placing a water prefab by dragging from Project panel to the Scene view. Note that this is using the Pro version of water (real-time reflection).

![](bbox=[0.324, 0.102, 0.931, 0.335])

**FIGURE 6.3** Placed water.

![](bbox=[0.324, 0.363, 0.932, 0.591])

**Step 7:** Play the game to check out the new water. Press the Play button (or press Ctrl-P on the PC or Command-P on the Mac) and walk around the scene to see how the water looks.

# Why?

Don't worry too much about how this looks quite yet. It's very likely that in the game view the water looks way too blue (even if you are using a Pro license). This is because the water is reflecting the sky, which at this point is just a flat blue. It will be prettier as we define the environment further.

# Skyboxes

Skyboxes are interesting things. In effect they paint a sky behind everything in your scene. The sky behaves visually as the real sky does (although generally not animated). There are a few things that are a little unintuitive about them though. First, a skybox is not a GameObject—it can't be seen in the Hierarchy panel. Skybox materials are chosen in the Render Settings (of all places), and then Cameras have the option of whether to draw them or not. Second, skyboxes don't affect any sort of lighting or baking. They are images that looks