# FIGURE 2.28

The Adaptive Degradation panel maintains a defined frame rate by degrading the rendering level.

![](bbox=[0.035, 0.22, 0.59, 0.52])

Different scene objects can degrade to different levels based on their priority. Object priority is set using a slider, which can be based on the object's distance from the camera, or Screen Size, which equates to the object's size in the viewport. If the slider is all the way to the left, then objects farther from the front of the scene are degraded first. If the slider is all the way to the right, then smaller objects are degraded first. Another option can force all objects smaller than a designated size to the lowest enabled display setting.

In the Maintain Frames Per Second field, you enter the frame rate that you want to maintain.

# Note

Remember that film generally runs at 24 fps, television at 30 fps, Web animations at 12 fps, and high-res games at 60 fps.

The FPS setting includes several options. The Draw Backfaces during Degrade option causes all object backfaces to appear. The Never Degrade Selected option keeps the selected object from changing its display setting and is a helpful option if you want a main character to remain displayed in its current display mode.

# Tip

If you have another unselected object in the scene that you want to keep visible, you can enable the Never Degrade option in the Object Properties dialog box. This option prevents the object from being degraded.

The Degrade to Default Lighting option turns off all lighting effects, which can be a display bottleneck and uses only default lighting. The Never Redraw After Degrade option prevents the viewports from being refreshed when the mouse button is released while Adaptive Degradation is enabled.