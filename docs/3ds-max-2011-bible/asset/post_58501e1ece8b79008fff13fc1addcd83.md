
the Arch & Design materials. Another benefit to the ProMaterials is that they are included in both 3ds Max and Autodesk's Revit, so users can share materials between the two packages.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_834_0.png)

Ambient Occlusion lets you light the scene by controlling the ambient light that gets bounced around the scene.

## Tip

Given that ProMaterials simulate real-world materials, they work best when they are used in a scene that includes photometric lights.

## Using the Car Paint material

When cars are painted in the factory, the paint is composed of two layers that give the car its unique look. The undercoat is called the flake layer, and it shines through the top layer. The mental ray Car Paint material includes settings for defining both of these layers. Figure 30.11 shows a car painted with this material.

## Combining bump and displacement maps

When mental ray is enabled, you can also take advantage of the Utility Bump and Displace Combiner materials. These materials let you combine up to three different bump or displacement maps into a single material. Each map has its own multiplier that is used to set its intensity.

## Using the Subsurface Scattering materials

The four mental ray materials that begin with “SSS” are Subsurface Scattering materials used to shade human skin. Skin has an interesting property that allows it to become slightly translucent when it is placed in front of a strong light source. The ears in particular are a good example of this because they allow light to penetrate and highlight their features. Most organic objects including leaves, rubber, milk, and skin can benefit from these materials.

## Part VII: Advanced Materials

## FIGURE 30.11

Cars rendered with the mental ray Car Paint shader use multiple layers, just like real cars.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_835_0.png)

## Cross-Ref

If you want more information on mental ray, check out Chapter 47, “Rendering with mental ray.”

## Summary

This chapter covered an assortment of specialized materials that enable specific types of effects. These specialized materials include matte/shadow, Ink ’n’ Paint, DirectX Shader, and the various mental ray materials including the Arch & Design, Car Paint, and Subsurface Scattering materials.

In this chapter, you’ve learned about the following:

- Using the matte/shadow material to hide objects
- Creating a cartoon rendering with the Ink ’n’ Paint materials
- Viewing game assets with the DirectX Shader
- Using the Arch & Design and ProMaterials materials
- Applying a multilayer car paint material
- Using the Subsurface Scattering materials

In the next chapter, you discover how the viewport can be made into a Canvas for painting directly on scene objects. The ability to render surface maps also is presented.

## FIGURE 31.1

The Viewport Canvas panel turns the viewport into a 2D painting canvas.

Black

Current color

![](img/ebbb4844f027f7d1c580e48108d2b6cb_837_0.png)

White

Open Color Palette

## Setting up an object for painting

The Canvas requires some setup before you can use it. The Viewport Canvas can be used on any object that has mapping coordinates. Mapping coordinates are applied to a primitive object by enabling the Generate Mapping Coordinates option in the Command Panel or by adding the UVW Mapping or UVW Unwrap modifier to an object.

## New Feature

The Viewport Canvas feature in the previous version of Max was allowed only on Editable Poly objects, but any object can be painted with this new version.

## Chapter 31: Painting in the Viewpoint Canvas and Rendering Surface Maps

With an object selected, select one of the brushes in the Canvas palette; if the object has a material with a bitmap applied, you can begin painting right away. If the object doesn't have a material or a texture applied, then the Assign Material dialog box appears, as shown in Figure 31.2.

## FIGURE 31.2

The Assign Material dialog box lets you choose the channel to paint on.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_838_0.png)

The Assign Standard Material button pops up a list of available channels where the texture may be applied using the Standard material. The Browse Material to Assign button opens the Material/Map Browser, where you can choose the type of material to use. The list of available channels includes Ambient Color, Diffuse Color, Specular Color, Specular Level, Glossiness, Self-Illumination, Opacity, Filter Color, Bump, Reflection, Refraction, and Displacement. After choosing a texture channel, the Create Texture dialog box appears, as shown in Figure 31.3, where you can set the size of the texture map and specify where the texture is saved, or you can select an existing texture. If a new texture is created, you need to specify a path and name for the new texture file. The texture is automatically mapped to the selected channel for the object's material. The Color setting is used for the texture's initial background color.

## FIGURE 31.3

The Create Texture dialog box automates the process of applying a material with a texture.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_838_1.png)

## Using the Canvas brushes

After the texture is set up, you can begin painting by clicking the Paint brush icon and dragging in the viewport over the selected object. Using the settings under the brush icons, you can set the Color, Radius, Opacity, Hardness, Spacing, Scatter, and Blur/Sharpen values. The available settings change depending on the brush selected.

When a brush is selected, it is highlighted in the Viewport Canvas palette and remains active until another brush is selected or until you right-click in the viewport. Table 31.1 lists the available brushes and layer tools.

## TABLE 31.1

## Viewport Canvas Brush Icons

| Palette Icon | Name | Description |
|---|---|---|
|  | Paint | Applies paint using the selected color or image. |
|  | Erase | Removes paint applied from any of the brushes on the selected layer, but not from the background layer. |
|  | Clone | Copies paint from another part of the current texture. Click with the Alt key held down to set the copy point. A green dot marks the copy location. Within the Paint Behavior rollout, you can select the Clone Source to be the Current Layer, All Layers, or the Viewport. |
|  | Fill | Fills the entire texture with paint. If you’re painting with an image, you can set the image to Tile or to 3D Wrap using the options in the Paint Behavior rollout. |
|  | Gradient | Lets you drag to extend a gradient across the surface of the object. Full color (or image) is painted where you first click and full transparency is painted where you stop dragging. The orientation of the gradient is aligned to the direction that you drag. |
|  | Blur | Blurs the area under the brush. |
|  | Sharper | Sharpens the area under the brush. |
|  | Contrast | Increases the contrast of the area under the brush. |
|  | Dodge | Lightens the area under the brush. |
|  | Burn | Darkens the area under the brush. |
|  | Smudge | Distorts and smudges the area under the brush. |
|  | Move Layer | Allows the current layer to be moved. |
|  | Rotate Layer | Allows the current layer to be rotated about the texture’s center. |
|  | Scale Layer | Allows the current layer to be scaled about the texture’s center. |

## Caution

The Background layer cannot be moved, rotated, or scaled.

## Chapter 31: Painting in the Viewpoint Canvas and Rendering Surface Maps

If the Paint brush is selected, you can immediately switch to the Erase brush by holding down the Shift key. Holding down the Ctrl key lets you click to select a different color from the current texture. Pressing the Spacebar causes a straight line to be drawn from the last painted location to the current cursor location. The Spacebar shortcut also works with the Eraser brush.

With any of the standard brushes, you can hold down the Ctrl+Shift keys to drag and change the brush radius. The Alt+Shift keys change the brush Opacity, and the Ctrl+Alt keys change the brush's Hardness value.

Clicking the Color swatch opens a Color Selector dialog box where you can choose a new color. You also can load a custom color palette using the Open Color Palette button or quickly switch between black and white colors, which is helpful for painting value maps.

At any time while painting, you are free in the viewport to rotate the model around to paint in a different location.

If you don't like the results after the painted texture has been applied to the object, click the Undo/Redo button to remove the last set of changes. Clicking the Undo/Redo button again reapplies the recent changes.

## Painting with images

In the Brush Images rollout are two swatches for selecting an image and a mask to paint with. Clicking the swatches opens a palette of presets, as shown in Figure 31.4. Clicking the Browse Custom Maps Directory button opens Windows Explorer to the Viewport Canvas folder where Max is installed. Within this folder are all the custom images and masks that are included in the palette.

## FIGURE 31.4

Custom images and masks can be added to the available presets in the Viewport Canvas.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_840_0.png)

Placing a new image or an image with an alpha channel (for masks) in this folder makes them appear in the presets palette and allows you to select and paint with them. The Reload Custom Maps button reloads any images placed in the folder so they can be seen.

To use an image or a mask, simply enable the Use option next to each. You also have several Rotation options including None, Random, and Follow Stroke. Figure 31.5 shows examples of each painting with stars. The left eye shows the None option, and all stars are oriented exactly the same. The right eye shows the Random option with each star oriented differently; the lower line shows the Follow Stroke option with the stars aligned in the direction of the brush stroke.
