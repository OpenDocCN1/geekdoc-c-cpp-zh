
## FIGURE 17.28

The Composite Layers rollout lists each composite map as a separate layer.

Hide the mask on this layer

Delete this layer

Add a new layer

Rename this layer

Color correct this mask

Hide this layer

Duplicate this layer

![](img/ebbb4844f027f7d1c580e48108d2b6cb_536_0.png)

Color correct this layer

Blending modes

Texture Preview

Mask preview

### Note

Composite maps and blending modes in 3ds Max 2009 work similar to layers in Photoshop.

Figure 17.29 shows three different uses for the Composite map. The left image combines a Checker map with a Gradient map. The last two images combine a Swirl map with Checker and Cellular maps.

## FIGURE 17.29

The Composite map can use multiple maps.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_536_1.png)

## Mask map

In the Mask Parameters rollout, you can select one map to use as a Mask and another one to display through the holes in the mask simply called Map. You also have an option to Invert the Mask. The black areas of the masking map are the areas that hide the underlying map. The white areas allow the underlying map to show through. The result of the Mask map is visible only when rendered.

## Mix map

You can use the Mix map to combine two maps or colors. It is similar to the Composite map, except that it uses a Mix Amount value to combine the two colors or maps instead of using the alpha channel. In the Mix Parameters rollout, the Mix Amount value of 0 includes only Color #1, and a value of 100 includes only Color #2. You can also use a Mixing Curve to define how the colors are mixed. The curve shape is controlled by altering its Upper and Lower values.

Figure 17.30 shows the Mix map with Perlin Marble and Checker maps applied as sub-maps and Mix values (from left to right) 25, 50, and 75.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_537_0.png)

## RGB Multiply map

The RGB Multiply map multiplies the RGB values for two separate maps and combines them to create a single map. Did you notice in the preceding figure that the Mix map fades both maps? The RGB Multiply map keeps the saturation of the individual maps by using each map’s alpha channel to combine the maps.

The RGB Multiply Parameters rollout includes an option to use the Alpha from either Map #1 or Map #2 or to Multiply the Alphas.

Figure 17.31 shows three samples of the RGB Multiply map. Each of these images combines a Wood map with (from left to right) a Checker map, a Gradient map, and a Stucco map. Notice that the colors aren’t faded for this map type.

## Color Modifier maps

You can use this group of maps to change the color of different materials. Color Modifier map types include Output, RGB Tint, and Vertex Color.

## FIGURE 17.31

The RGB Multiply map combines maps at full saturation using alpha channels.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_538_0.png)

## Color Correction map

The Color Correction map lets you change the colors of a texture. The corrections are applied using a stack approach. The Color Correction map includes four rollouts: Basic Parameters, Channels, Color, and Lightness, as shown in Figure 17.32, and each of these settings is in order starting from the top rollout.

The Basic Parameters rollout includes a color swatch and a map button that you can use to specify the color to affect the map. In the Channels rollout, you can select to make the map Normal, Monochrome, Invert, or Custom. If Custom is selected, then you can specify a specific color for each of the RGB and alpha channels. The available channel options are Red, Green, Blue, Alpha, the inverse for each, Monochrome, One, and Zero.

In the Color rollout, you can adjust the Hue Shift, Saturation, Hue Tint, and Strength for the map, and the Lightness rollout gives you two options: Standard and Advanced. In Standard mode, you can adjust the Brightness and Contrast using simple sliders, but Advanced mode gives you control over the Gain, F-Stops, and Printer Lights settings for each channel.

## Output map

The Output map provides a way to add the functions of the Output rollout to maps that don't include an output rollout. Details on this map type are presented in the earlier section that covers the Output rollout.

## RGB Tint map

The RGB Tint map includes color swatches for the red, green, and blue channel values. Adjusting these colors alters the amount of tint in the map. For example, setting the red color swatch in the RGB Tint Parameters rollout to white and the green and blue color swatches to black creates a map with a heavy red tint. You can also load maps in place of the colors.

## Vertex Color map

The Vertex Color map makes the vertex colors assigned to an Editable Mesh, Poly, or Patch object visible when the object is rendered. When an Editable Mesh, Poly, or Patch object is in Vertex subobject mode, you can assign the selected vertices a Color, an Illumination color, and an Alpha value. These settings are in the Surface Properties rollout. You can also assign vertex colors using the Assign Vertex Colors utility. Use this utility to assign color to the current object or to assign material colors to the object's vertices using the given lights. A third way to assign vertex colors is with the Vertex Paint modifier, which you access using the Modifiers* Mesh Editing* Vertex Paint menu command. This modifier lets you color vertices by painting directly on an object.

## FIGURE 17.32

The Color Correction map lets you work with textures as if you had a photo lab.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_539_0.png)

## Cross-Ref

For more detail on the Vertex Paint modifier, see Chapter 18, “Creating Compound Materials and Using Material Modifiers.”

After vertex colors are assigned, you need to apply the Vertex Color map to the diffuse color in the Material Editor and apply it to the object for the object to render the vertex colors. This map doesn't have any settings.

## Miscellaneous maps

These maps are actually grouped into a category called Other, but they mostly deal with reflection and refraction effects. Maps in this category include Camera Map Per Pixel, Flat Mirror, Normal Bump, Raytrace, Reflect/Refract, and Thin Wall Refraction.

## Camera Map Per Pixel map

The Camera Map Per Pixel map lets you project a map from the location of a camera. You use this map by rendering the scene, editing the rendered image in an image-editing program, and projecting the image back onto the scene.

The Camera Map Parameters rollout includes buttons that let you select the Camera, Texture, ZBuffer Mask, and Mask.

## Flat Mirror map

The Flat Mirror map reflects the surroundings using a coplanar group of faces. In the Flat Mirror Parameters rollout, you can select a Blur amount to apply. You can specify whether to Render the First Frame Only or Every Nth Frame. You also have an option to Use the Environment Map or to apply to Faces with a given ID.

### Note

Flat Mirror maps are applied only to selected coplanar faces using the material ID.

The Distortion options include None, Use Bump Map, and Use Built-In Noise. If the Bump Map option is selected, you can define a Distortion Amount. If the Noise option is selected, you can choose Regular, Fractal, or Turbulence noise types with Phase, Size, and Levels values.

## Tutorial: Creating a mirror surface

Mirror, mirror on the wall, who’s the best modeler of them all? Using the Flat Mirror map, you can create, believe it or not, mirrors. To create and configure a flat mirror map, follow these steps:

- 1. Open the Reflection in mirror.max file from the Chap 17 directory on the DVD.
This file includes a mesh of a man standing in front of a mirror. The mirror subobject faces have been selected and assigned a material ID of 1.

- 2. Choose Rendering→ Material Editor→ Slate Material Editor (or press the M key) to open the Material Editor.

- 3. Locate and double-click the Flat Mirror option in the Material/Map Browser to add a node to the Node View. Drag a connection wire from the output socket, drop it anywhere on the Node View, and then select the Materials/Standard material from the pop-up menu and the Reflection channel from the parameters pop-up menu. This adds a standard material node to the Node View and connects the Flat Mirror node to the material’s Reflection parameter.

### Note

If the Flat Mirror map isn’t available, select the Map radio button in the Show section.

- 4. Double-click the Flat Mirror node to make its parameters appear in the Parameter Editor. In the Flat Mirror Parameters rollout, deselect the Apply Blur and Use Environment Map options and select the Apply to Faces with ID option. Then set the ID value to 1.

- 5. Drag the material node’s output socket to the mirror object in the viewport to apply the material to the mirror.

Figure 17.33 shows a model being reflected off a simple patch object with a Flat Mirror map applied to it. The reflection is visible only in the final rendered image.

## Normal Bump map

The Normal Bump map lets you alter the appearance of the details on the surface using a Normal map. Normal maps can be created using the Render to Texture dialog box. The Parameters rollout for this map type lets you specify a normal map along with another additional bump map. You also can set the amount each map is displaced. Additional options let you flip and swap the red and green channel directions, which define the X and Y axes.
