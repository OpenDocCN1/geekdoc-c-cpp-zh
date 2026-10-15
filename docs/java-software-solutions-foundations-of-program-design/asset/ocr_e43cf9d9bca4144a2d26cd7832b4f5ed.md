![](bbox=[0.26, 0.11, 0.87, 0.47])

# FIGURE J.1 A sketch of the user interface for the PaintBox program

with the client. For other systems there may be many such sketches for each screen of the program.

The interface sketch shows a main drawing area where the user will create a drawing. The top edge contains a set of buttons used to select various tools, such as the oval tool to draw an oval or circle, the color tool to change the current drawing color, and a select tool to select a previously drawn shape to modify or move it. Two menu headings are shown along the top edge. The File menu contains operations to begin a new drawing, save a drawing, and exit the program. The Edit menu contains editing operations such as cut, copy, and paste.

As a result of the discussions with the client, several additional requirements issues are established:

+   - There is no need to have separate user interactions for circles or squares because they are subsets of ovals and rectangles, respectively.
+   - The user should also be able to create polyline shapes.
+   - The buttons used to select drawing tools should have icons instead of words.