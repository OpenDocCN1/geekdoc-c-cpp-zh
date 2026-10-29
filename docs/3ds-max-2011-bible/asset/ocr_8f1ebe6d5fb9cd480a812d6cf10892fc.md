# Loading viewport background images

The Views ▸ Viewport Background ▸ Viewport Background menu command (Alt+B) opens a dialog box, shown in Figure 2.34, in which you can select an image or animation to appear behind a viewport. Each viewport can have a different background image. The displayed background image is helpful for aligning objects in a scene, but it is for display purposes only and will not be rendered. To create a background image to be rendered, you need to specify the background in the Environment dialog box, opened using the Rendering ▸ Environment (keyboard shortcut, 8) menu command.

If the background image changes, you can update the viewport using the Views ▸ Viewport Background ▸ Update Background Image menu command (Alt+Shift+Ctrl+B). This is helpful if you have the background image opened in Photoshop at the same time. You can update the background image, save it, and then immediately update the image in Max. The Views Viewport Background ▸ Reset Background Transform menu command automatically rescales and recenteres the background image to fit the viewport. You should use this if you’ve changed the viewport size or changed the background’s size.

The Files button in the Viewport Background dialog box opens the Select Background Image dialog box, where you can select the image to load. The Devices button lets you obtain a background from a device such as a Video Recorder. If an environment map is already loaded into the Environment dialog box, you can simply click the Use Environment Background option. Keep in mind that the background image will not be rendered unless it is made into an Environment map.

# Cross-Ref

Environment maps are covered in Chapter 23, “Rendering a Scene and Enabling Quicksilver.”

# Loading viewport background animations

The Animation Synchronization section of the Viewport Background dialog box lets you set which frames of a background animation sequence are displayed. The Use Frame and To values determine which frames of the loaded animation are used. The Step value trims the number of frames that are to be used by selecting every Nth frame. For example, a Step value of 4 would use every fourth frame.

# Tip

Loading an animation sequence as a viewport background can really help as you begin to animate complex motions, like a running horse. By stepping through the frames of the animation, you can line up your model with the background image for realistic animations.

The Start At value is the frame in the current scene where this background animation would first appear. The Sync Start to Frame value is the frame of the background animation that should appear first. The Start and End Processing options let you determine what appears before the Start and End frames. Options include displaying a blank, holding the current frame, and looping.

If you select an animation as the background, make sure that the Animate Background option is selected. Also note that the viewport background is not visible if the Display Background option is not selected.

The Aspect Ratio section offers options for setting the size of the background image. You can select to Match Viewport, Match Bitmap, or Match Rendering Output.

The Lock Zoom/Pan option is available if either the Match Bitmap option or the Match Rendering Output option is selected. This option locks the background image to the geometry so that when the objects in the scene are zoomed or panned, the background image follows. If the background gets out of line, you can reset its position with the Views ▸ Viewport Background ▸ Reset Background Transform command.