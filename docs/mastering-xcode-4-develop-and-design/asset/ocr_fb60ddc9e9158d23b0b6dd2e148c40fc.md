![](bbox=[0.127, 0.174, 0.718, 0.456])

# THE EDITOR AREA

The Editor area (Figure 5.2) is where you construct the interface. This involves dragging interface elements from the Utility area’s object library into the canvas (the grid area) of the Editor and sizing and positioning them as needed. You can also create interface elements and controller objects by dragging them into the Dock, immediately to the left of the canvas.

The dock bar along the left side of the Editor (to the left of the grid) in Figure 5.2 is expanded to show more detail about the objects contained in the xib. Use the button at the bottom of the dock to expand or collapse the dock.

Only user interface elements (such as buttons and windows) can be dragged into the canvas. Instances of controllers aren’t part of the user interface but are created or represented in the nib to serve as a connection point between the UI and your code; therefore, they exist only in the Dock.

You can make connections to outlets by holding down the Control key and dragging from the controller in which the outlet is defined to the desired interface element. The controller could be File’s Owner (the controller to which the contents of the nib belong) or some other controller object that you’ve instantiated in your nib.