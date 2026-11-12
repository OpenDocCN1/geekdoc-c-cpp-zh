![](bbox=[0.18, 0.1, 0.55, 0.33])

**FIGURE 2.13** Comparison between original output and layered approach.

# Housekeeping

**Step 15:** Save again. Be sure you're saving as EntryWayWallsInnerNormalRaw.

# Why?

Since this strange bluish image makes it pretty tough to know what the result will look like, it will be important to have the raw version to come back to if the final result in Unity is not what was planned.

**Step 16:** Flatten the image (Layer>Flatten Image).

# Why?

We will need to "normalize" the image to bring the normal vectors back into the needed value of 1, but this needs to be done to the total image and not just one layer.

**Step 17:** Normalize the image. Choose Filter>NVidia Tools>NormalMapFilter. In the Alternate Conversion area check Normalize Only. Press OK.

# Why?

The other settings can all remain the same because none of them will be used. Normalize Only will ensure the red, green, and blue normal vectors are exactly 1 and thus ready to be a normal map.

**Step 18:** Save the image for use in Unity. Save the file as EntryWay_WallsInner_Normal into the Incursion-Unity/Assets/EntryWay.fbm. The file format can be whatever you'd like (I saved it as a .psd).

# Why?

Due to our deft use of manual exporting, all the texture files related to the EntryWay are in this EntryWay.fbm folder that Unity created. Adding any new texture assets that are meant for EntryWay keeps the Project panel clean.