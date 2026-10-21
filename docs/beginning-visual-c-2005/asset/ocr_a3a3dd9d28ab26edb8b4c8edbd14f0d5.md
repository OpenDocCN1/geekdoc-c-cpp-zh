A toolbar button is a 16x15 array of pixels that contains a pictorial representation of the function it operates. You can see in Figure 13-12 that the resource editor provides an enlarged view of a toolbar button so that you can see and manipulate individual pixels. If you click the new button at the right end of the row as indicated, you’ll be able to draw this button. Before starting the editing, drag the new button about half a button width to the right. It separates from its neighbor on the left to start a new block.

You should keep the toolbar button blocks in the same sequence as the items on the menu bar, so you’ll create the element type selection buttons first. You’ll be using the following editing buttons provided by the resource editor that appear in the toolbar for the Visual C++ 2005 application window.

+   - Pencil for drawing individual pixels
+   - Eraser for erasing individual pixels
+   - Fill an area with the current color
+   - Zoom the view of the button
+   - Draw a rectangle
+   - Draw an ellipse
+   - Draw a curve

If it is not already visible, you can display the window for selecting a color by right-clicking a toolbar button and selecting Show Colors Window from the pop-up. Make sure that the black color is selected and use the pencil tool to draw a diagonal line in the enlarged image of the new toolbar button. In fact, if you want it a bit bigger, you can use the Magnification Tool editing button to enlarge it up to eight times its actual size. If you make a mistake, you can change to the Erase Tool editing button, but you need to make sure that the color selected corresponds to the background color for the button you are editing. You can also erase individual pixels by clicking them using the right mouse button, but again you need to be sure that the background color is set correctly when you do this. To set the background color, just click the appropriate color using the right mouse button. After you’re happy with what you’ve drawn, the next step is to edit the toolbar button properties.

# Editing Toolbar Button Properties

Double-click your new button in the toolbar to bring up its properties window, as shown in Figure 13-13.

The properties box shows a default ID for the button, but you want to associate the button with the menu item Element > Line that we’ve already defined, so click ID and then click the down arrow to display alternative values. You can then select ID_ELEMENT_LINE from the drop-down box. If you click on Prompt you’ll find that this also causes the same prompt to appear in the status bar because the prompt is recorded along with the ID. You can close the Properties window to complete the button definition.

You can now move on to designing the other three element buttons. You can use the rectangle editing button to draw a rectangle and the ellipse button to draw a circle. You can draw a curve using the pencil to set individual pixels, or use the curve button. You need to associate each button with the ID corresponding to the equivalent menu item that you defined earlier.