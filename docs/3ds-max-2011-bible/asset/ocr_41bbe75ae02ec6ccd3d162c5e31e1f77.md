# Working with a ring array

You can find the Ring Array system by opening the Create panel and selecting the Systems category. Clicking the Ring Array button opens a Parameters rollout. In this rollout are parameters for the ring’s Radius, Amplitude, Cycles, Phase, and the Number of elements to include.

You create the actual array by clicking and dragging in one of the viewports. Initially, all elements are simple box objects surrounding a green dummy object.

The Amplitude, Cycles, and Phase values define the sinusoidal nature of the circle. The Amplitude is the maximum distance that you can position the objects from the horizontal plane. If the Amplitude is set to 0, then all objects lie in the same horizontal plane. The Cycles value is the number of waves that occur around the entire circle. The Phase determines which position along the circle starts in the up position.

# Tutorial: Using Ring Array to create a carousel

Continuing with the theme park attractions motif, this example creates a carousel. The horse model comes from Poser but was simplified using the MultiRes modifier.

To use a Ring Array system to create a carousel, follow these steps:

+   1. Open the Carousel.max file from the Chap 08 directory on the DVD. This file includes a carousel structure made from primitives along with a carousel horse.
+   2. Open the Create panel, select the Systems category, and click the Ring Array button. Drag in the Top viewport from the center of the carousel to create a ring array. Then enter a Radius value of 250, an Amplitude of 20, a Cycles value of 3, and a Number value of 6. Then right-click in the active viewport to deselect the Ring Array tool.

# Note

If the Ring Array object gets deselected, you can access its parameters in the Motion panel, not in the Modify panel.

+   3. Select the Ring Array’s Dummy object in the Left viewport, select the Tools▸Align▸Align menu command, and then click on the center cylinder. The Align Selection dialog box opens. Enable the X, Y, and Z Position options and choose the Center options for both the Current and Target objects and click the Apply button. This aligns the ring array to the center of the carousel.
+   4. Select the horse object, and choose the Tools▸Align▸Clone and Align menu command. In the Clone and Align dialog box that opens, select the Instant options along with the X, Y, and Z Position and Orientation options. Then click the Pick button and click on each of the boxes in the ring array. Set the Offset values for the X and Y Orientation values to 90 to fix the orientation of the placed horses. Then click the Apply button and close the Clone and Align dialog box.

Figure 8.16 shows the finished carousel. Notice that each horse is at a different height. Once the horses are placed, you can delete or hide the Ring Array object.