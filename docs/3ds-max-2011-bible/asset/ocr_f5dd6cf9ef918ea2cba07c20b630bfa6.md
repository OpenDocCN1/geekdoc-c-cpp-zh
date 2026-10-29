# Part 1: Getting Started with 3ds Max

# Tip

Another way to speed the frame rate in the active viewport is to disable (D) the inactive viewports.

To enable Adaptive Degradation in the viewports, follow these steps:

+   1. Open the Delfino Feroce 2001.max file from the Chap 02 directory on the DVD. This file includes a realistic car model created by Viewpoint Databals.
+   
+   2. Select the Edit > Select All (Ctrl+A) menu command to select all the car's objects.
+   
+   3. Hold down the Shift key and drag the car with the Select and Move tool. In the Clone Options dialog box that opens, enter a value of 5 for the Number of Copies. If your computer is fast enough to display all copies of the car without any trouble, try increasing the number of copies. This creates five more copies of the selected car.
+   
+   4. Right-click the Adaptive Degradation button at the bottom of the interface. In the Adaptive Degradation panel of the Viewport Configuration dialog box, set the Maintain Frames Per Second value to 25, enable the Use Current Display Mode, Wireframe, and Bounding Box options, and drag the slider to the left to the Distance from Camera side. Then click OK. Click the Adaptive Degradation button to enable it. The Adaptive Degradation button turns yellow when enabled.
+   
+   5. Click the Arc Rotate button in the Viewport Navigation Controls and drag in the viewport. Notice how the cars farthest from the camera are degraded to bounding boxes.
+   
+   6. Right-click the Adaptive Degradation button and drag the slider all the way to the right so that Screen Size affects what is degraded. Then close the Viewport Configuration dialog box and drag in the viewport again. Notice this time how the smaller objects are degraded, as shown in Figure 2.29.

# Tip

Pressing the 7 key enables statistics mode in the viewport so you can see in real time the frames per second.

# Defining regions

The Regions panel enables you to define regions and focus your rendering energies on a smaller area. Complex scenes can take considerable time and machine power to render. Sometimes, you want to test render only a portion of a viewport to check material assignment, texture map placement, or lighting.

You can define the size of the various Regions in the Regions panel of the Viewport Configuration dialog box, shown in Figure 2.30.

After you've specified a Blowup Region or a Sub Region, you can select to render using these regions by selecting Region or Blowup from the Render Frame Window and clicking the Render button. If you click the Edit Region button, the specified region is displayed as an outline in the viewport. You can move this outline to reposition it or drag its edge or corner handles to resize the region. The new position and dimension values are updated in the Regions panel for next time. Click the Render button to begin the rendering process.

The difference between these two regions is that the Sub Region displays the Rendered Frame Window in black, except for the specified subregion. The Blowup Region fills the entire Rendered Frame Window, as shown in Figure 2.31.