# Unity Games by Tutorials

# Chapter 12: Beginning Unity 2D

| Texture Type | Sprite (2D and UI) |
|---|---|
| Texture Shape | 2D |
| Sprite Mode | Multiple |
| Packing Tag | |
| Pixels Per Unit | 100 |
| Mesh Type | Tight |
| Extrude Edges | 1 |
| Generate Physics Shape | |

Click the Sprite Editor button to open its window. You'll see an enlarged view of the spritesheet.

![](bbox=[0.197, 0.327, 0.802, 0.497])

You have a few options for slicing a spritesheet into individual sub-sprites. For this exercise, you'll use the Grid By Cell Size method, but you will learn about the others in a few moments. With this method, you enter the pixel size of each "cut-out" sprite, as well as offset and padding.

Click the Slice drop-down in the top-left of the Sprite editor and change Type to Grid By Cell Size. Set Pixel Size to (48, 40) and leave the other options as is. All Super Soy animation frames are 48 x 40 pixels. Hence, you're using the same values for grid slicing. Click Slice to, well, slice.

| Grid By Cell Size | |
|---|---|
| Pixel Size | X 48 Y 40 |
| Offset | X 0 Y 0 |
| Padding | X 0 Y 0 |
| Pivot | Center |
| Custom Pivot | Slice |

Look at the Sprite editor. You should see bounding boxes around the sprites that show where the grid slice was applied.

raywenderlich.com

332