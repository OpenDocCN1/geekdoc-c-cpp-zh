
# FIGURE 31.5

The image rotation options determine how the stars are oriented.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_841_0.png)

Within the Brush Image Settings rollout are some options for setting how the image is projected onto the object. The options include Hit Normal and From Screen. The Hit Normal option applies the image as if projected down onto the normal of the object. The From Screen option applies the texture as if projected from the screen position onto the object. Other options make the image fit within the brush size and offer tiling options of None, Tile, and Across Screen.

## Using paint layers

The Viewport Canvas palette lets you paint on layers just like you can in Photoshop. To access the layers, click the Layers Dialog button in the Viewport Canvas dialog box. The Layers palette, shown in Figure 31.6, shows the current layers in a stack. Each layer can be named, and the layers are placed on the object with the top layers appearing on top of the lower layers. You also can select a blend method and an Opacity value. The buttons at the bottom of the Layers palette let you create new layers, duplicate the current layer, or delete a layer. The small light bulb icon to the left of the layer name lets you turn a layer on or off.

When a layer other than the Background layer is selected, you can use the Layer tool icons located at the top of the Viewport Canvas palette. These Layer tools let you move, rotate, and/or scale the current layer.

## Chapter 31: Painting in the Viewport Canvas and Rendering Surface Maps

# FIGURE 31.6

The Layers palette lets you work with layers for the current texture.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_842_0.png)

Blend method

Duplicate Layer

Add New Layer

Delete Layer

## Caution

Be aware that you cannot erase any paint applied to the Background layer using the Erase tool. ■

The Layers palette includes some menus that have many of the same commands found in Photoshop. For example, you can use the Layer menu to add layer masks, merge a layer down, flip a layer either horizontally or vertically, or flatten all visible layers.

The Adjust menu includes options for changing the Brightness, Contrast, Hue, Saturation, Levels, or Color Balance. You also get an Auto Levels option. The Filter menu includes filters for blurring, sharpening, finding edges, median, threshold, high pass, and distort.

Within the File menu are options for pasting from the clipboard, loading a bitmap into the current layer, saving the current bitmap (as a flattened file), or saving the image with all layers to a PSD file that can be reopened in Photoshop.

## Tip

If you want to maintain the various layers after you’re finished painting, be sure to save your texture using an image format that supports layers, such as PSD. ■

If you’ve added any layers to your texture and you exit the Canvas, the Save Texture Layers dialog box, shown in Figure 31.7, opens. Using this dialog box, you can choose to continue painting, save the file as a PSD file, which maintains the various layers, flatten all layers and save the texture, save and replace, save, flatten and then save again, or simply discard. If you plan to revisit the layers of your texture, save it as a PSD file, but if you’re happy with the results, you can flatten and save the texture.

## Part VII: Advanced Materials

# FIGURE 31.7

The Save Texture Layers dialog box lets you maintain the various texture layers.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_843_0.png)

## Painting in 2D

Painting directly on a 3D object has its advantages, but when painting over a random surface, the results can be irregular. The Viewport Canvas dialog box includes a 2D painting mode that displays the current texture in a rectangular window and lets you paint directly on the texture. This is helpful for textures that need to be projected onto an object such as those with text.

To access the 2D painting mode, simply click the 2D View button under the colors and the current texture is opened in a window, as shown in Figure 31.8. The buttons at the top of this window let you see the UV wireframes, fit the texture in the view, or view the image at its actual size. Any changes made to the texture in 2D painting mode are immediately reflected on the selected object in the viewports.

Clicking the 2D View button again toggles the 2D painting mode off, and the 2D Paint window closes.

## Using the paint options

When the Viewport Canvas palette is open, several additional rollouts hold the options that affect the various brushes and texture. Within the Options rollout, you can select which map type and channel to paint on. There is also an option to Save Texture. If this option is disabled, any paint applied to the texture isn't saved. This lets you try a different look without saving it. You can also do this by painting on a new layer that could be deleted. The Brush Preview option shows the outline and size of the brush as you paint.

Within the Paint Behavior rollout are options to have the paint affect any area of the object within the brush's spherical radius or to apply the paint through the entire object with the Depth option. The Mirroring options let you mirror all paint strokes across the X, Y, or Z axes.

The Randomize rollout, shown in Figure 31.9, lets you set the minimum and maximum values for several different settings including Brush Radius, Opacity, Spacing, Scatter, and Color.

## Chapter 31: Painting in the Viewport Canvas and Rendering Surface Maps

# FIGURE 31.8

2D painting mode lets you paint directly on the texture without any perspective distortion.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_844_0.png)

# FIGURE 31.9

Using the Randomize rollout, you can add variety to the texture.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_844_1.png)

Using the Table Pressure rollout, you can select which attributes are affected by an increase in the tablet pressure. The options include Brush Radius, Opacity, Hardness, and Scatter.

## Part VII: Advanced Materials

The Load/Save Settings rollout includes buttons for saving and loading the Viewport Canvas settings. Settings are saved using a simple text file. There is also a button for saving the current settings as the default.

## Tutorial: Face painting

To show off the Viewport Canvas, we do some face painting on a women's head model. This model was created by Zygote Media and is a good example of a high-res model.

To paint on a character's face using the Viewport Canvas, follow these steps:

- 1. Open the Face painting.max file from the Chap 31 directory on the DVD. This file includes a women's head mesh created by Zygote Media.
- 2. Rotate the head model so the cheek is clearly visible, apply the UVW Map modifier to make sure the object has mapping coordinates with the Planar map, and click the View Align button.
- 3. Open the Viewport Canvas panel with the Tools⋗Viewport Canvas menu command.
- 4. Select the model, and click the Paint Brush icon in the Viewport Canvas panel, then select the Diffuse Color option in the pop-up menu. In the Create Texture dialog box that pops up next, select the 512 × 512 preset and click the file button next to the Save New Texture field to open the file dialog box. Save the file as Face Painting texture.tif, and click the OK button.
- 5. Set the brush Radius to 32, the blending mode to Normal, and the Opacity to 100, and choose a bright red color. Then click the Brush icon, and draw a heart on the women's cheek. Then click the Paint icon again to apply the texture to the model.

Figure 31.10 shows the resulting applied texture.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_845_0.png)

## Using Vertex Colors

Another similar feature to the Viewport Canvas is the Vertex Paint modifier. This modifier lets you apply colors to a model without the weight of a texture. When creating models for games, the size of the texture map can be prohibitive. I mean, what model that weighs in at 16KB or less wants to carry around a 2MB texture map? The solution that much of the gaming world relies on is to apply a single color to a vertex. Having each vertex remember its color (or even several colors) requires very little additional information for the mesh and can create some good shading. Colors are then interpolated across the face of the polygon between two different colors on adjacent vertices.

The results aren’t as clean and detailed as texture maps, but for their size, vertex colors are worth the price.

## Assigning vertex colors

Vertex colors can be assigned in the Surface Properties rollout for Editable Mesh and Editable Patch objects, and in the Vertex and Polygon Properties rollouts for Editable Poly objects. They also can be assigned in Face, Polygon, and Element subobject modes using a little rollout section called Edit Vertex Colors. Within this section are two color swatches for selecting Color and Illumination values. The Alpha value sets the alpha transparency value for the vertex.

## Painting vertices with the Vertex Paint modifier

Another, more interactive way to color vertices is with the Vertex Paint modifier. This modifier lets you paint on an object by specifying a color for each vertex. If adjacent vertices have different colors assigned, a gradient is created across the face. The benefit of this coloring option is that it is very efficient and requires almost no memory.

The Vertex Paint modifier lets you specify a color and paint directly on the surface of an object by painting the vertices. The color is applied with a paintbrush-shaped cursor. The modifier can be applied multiple times to an object, giving you the ability to blend several layers of vertex paints together. You can find this modifier in the Modifiers ➜ Mesh Editing submenu.

## Note

After the Vertex Paint modifier has been applied to an object, the Paintbox automatically reappears whenever the object is reselected.

Applying this modifier opens a Vertex Paint dialog box called the Paintbox, shown in Figure 31.11. At the top of the Paintbox are four icons that can be used to show the visible results of the painting in the viewports. The options include Vertex Color Display—Unshaded, Vertex Color Display—Shaded, Vertex Color Display, and Toggle Texture Display On/Off.

The Vertex Color icon lets you work on the Vertex Color, Illumination, Alpha, or any one of the 99 available map channels. The lock icon locks the display to the selected channel, or you could be looking at a different channel from the one you are painting.

The large Paint and Erase buttons let you add or remove vertex colors using the color specified in the color swatch. You also can select colors from objects in the viewports using the eyedropper tool and then set the Opacity.
