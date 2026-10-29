
## Camera type and display options

The Type option enables you to change a Free camera to a Target camera and then change back at any time.

The Show Cone option enables you to display the camera's cone, showing the boundaries of the camera view when the camera isn't selected. (The camera cone is always visible when a camera is selected.) The Show Horizon option sets a horizon line within the camera view, which is a dark gray line where the horizon is located.

## Environment ranges and clipping planes

You use the Near and Far Range values to specify the volume within which atmospheric effects like fog and volume lights are to be contained. The Show option causes these limits to be displayed as yellow rectangles within the camera's cone.

You use clipping planes to designate the closest and farthest object that the camera can see. In Max, they are displayed as red rectangles with crossing diagonals in the camera cone. If the Clip Manually option is disabled, then the clipping planes are set automatically with the Near Clip Plane set to 3 units. Figure 19.5 shows a camera with Clipping Planes specified. The front Clipping Plane intersects the car and chops off its front end. The far Clipping Plane is far behind the car.

### Tip

Clipping planes can be used to create a cutaway view of your model.

### FIGURE 19.5

A camera cone displaying Clipping Planes

![](img/ebbb4844f027f7d1c580e48108d2b6cb_577_0.png)

## Camera Correction modifier

To understand the Camera Correction modifier, you first need to understand what two-point perspective is. Default cameras in Max use three-point perspective, which causes all lines to converge to a vanishing point off in the distance, but two-point perspective causes all vertical lines to remain vertical.

The visual effect of this modifier is that extra-tall objects appear to bend toward the camera when corrected. For example, if you have a camera pointed at a skyscraper, then correcting the camera with the Camera Correction modifier makes the top of the building appear closer rather than having it recede away.

The Camera Correction modifier has an Amount value that lets you specify how much correction to apply and a Direction value that orients the angle of vertical lines in the scene. There is also a Guess button, which automatically sets the correction values for you based on the Z-axis vertical.

### Caution

The Camera Correction modifier doesn’t appear in the Modifier List in the Modifier Stack, but you can select it from the Modifiers ▸ Cameras menu.

## Creating multi-pass camera effects

All cameras have the option to enable them to become multi-pass cameras. You can find these settings in the Parameters rollout when a camera object is selected. Multi-pass cameras are created by checking the Enable button and selecting the effect from the drop-down list. The current available effects include Depth of Field (mental ray), Depth of Field, and Motion Blur. For each, an associated rollout of parameters opens.

### Cross-Ref

The Depth of Field (mental ray) effect option is covered in Chapter 47, “Rendering with mental ray.”

The Multi-Pass Effect section of the Parameters rollout also includes a Preview button. This button makes the effect visible in the viewports for the current frame. This feature can save you a significant amount of time that normally would be spent test-rendering the scene. The Preview button is worth its weight in render speed. Using this button, you can preview the effect without having to render the entire sequence.

### Caution

The Preview button does not work unless the Camera view is the active viewport.

The Render Effect Per Pass option causes any applied Render Effect to be applied at each pass. If disabled, then any applied Render Effect is applied after the passes are completed.

### Cross-Ref

You can also apply these multi-pass effects as Render Effects. See Chapter 46, “Using Atmospheric and Render Effects.”

## Using the Depth of Field effect

The Depth of Field Parameters rollout, shown in Figure 19.6, appears when the Depth of Field option is selected in the Multi-Pass Effect section of the Parameters rollout. It includes settings for controlling the Depth of Field multi-pass effect.

## Part IV: Materials, Cameras, and Lighting Basics

### FIGURE 19.6

Use the Depth of Field Parameters rollout to set the number of passes.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_579_0.png)

You can select to use the Target Distance (which is the distance to the camera's target), or you can specify a separate Focal Depth distance. This location is the point where the camera is in focus. All scene objects closer and farther from this location are blurred to an extent, depending on their distance from the focal point.

### Note

Even Free cameras have a Target Distance. This distance is displayed at the bottom of the Parameters rollout.

Within the Depth of Field Parameters rollout, you also have the option to display each separate pass in the Rendered Frame Window with the Display Passes option and to use the camera's original location for the first rendering pass by enabling the Use Original Location option.

The Total Passes is the number of times the scene is rendered to produce the effect, and the Sample Radius is the potential distance that the scene can move during the passes. By moving the scene about the radius value and re-rendering a pass, the object becomes blurred more away from the focal distance. If you have a fairly tight scene, the default Radius value does not produce very visible results. Try increasing the Sample Radius value and re-rendering. Figure 19.7 shows a scene with Sample Radius values of 1 and 5.

### FIGURE 19.7

Changing the Sample Radius value changes the amount of blur added to the scene.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_579_1.png)

### Note

The Depth of Field effect is applied only to rendered scene objects. It is not applied to any background images.

The Sample Bias value moves the blurring closer to the focal point (for higher values) or away from the focal point (for lower values). If you want to highlight the focal point and radically blur the other objects in the scene, set the Sample Bias to 1.0. A Sample Bias setting of 0 results in a more even blurring.

The Normalize Weights option allows you to control how the various passes are blended. When enabled, you can avoid streaking along the object edges. The Dither Strength value controls the amount of dither taking place. Higher Dither Strength values make the image grainier. The Tile Size value also controls dither by specifying the dither pattern size.

With lots of passes specified, the render time can be fairly steep. To lower the overall rendering time, you can disable the Anti-alias and filtering computations. These speed up the rendering time at the cost of image quality.

## Tutorial: Applying a Depth of Field effect to a row of windmills

In the dry plains of Southwest America, the wind blows fiercely. Rows of windmills are lined up in an effort to harness this energy. For this example, you use the Depth of Field effect to display the windmills.

To apply a Depth of Field effect to a row of windmills, follow these steps:

- 1. Open the Depth of field windmills.max file from the Chap 19 directory on the DVD. This file includes a windmill object (created by Viewpoint Datalabs) duplicated multiple times and positioned in a row.
- 2. Select Create > Cameras > Target Camera, and drag in the Top viewport from the lower-left corner to the center of the windmills. In the Left viewport, select the camera and move it upward, and then select the Camera Target and also move it upward to the upper third of the windmill's height, so the entire row of windmills can be seen. If the windmills don't fill the camera view, adjust the Field of View (FOV) setting.

### Tip

You can select both the camera and its target by clicking on the line that connects them.

- 3. Select the Perspective viewport, right-click on the viewport title, and select Views > Camera01 (or just press the C key) to make this viewport the Camera view.
- 4. With the Camera selected, open the Modify panel, enable the Multi-Pass Effect option, and then select Depth of Field in the drop-down list.
- 5. In the Depth of Field Parameters rollout, enable the Use Target Distance option and set the Total Passes to 15, the Sample Radius to 3.0, and the Sample Bias to 1.0.
- 6. Select the Camera viewport, and click the Preview button in the Parameters rollout. This shows the Depth of Field effect in the viewport.

Figure 19.8 shows the resulting Depth of Field effect in the viewport for the row of windmills.
