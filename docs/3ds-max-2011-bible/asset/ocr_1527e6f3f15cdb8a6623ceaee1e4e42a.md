# Part III: Modeling Basics

# Editing segments

To edit a segment, click the Segment subobject in the Modifier Stack or select the segment icon from the Selection rollout to enter segment subobject mode. Clicking again on either exits this mode. Segments are the lines or edges that run between two vertices. Many of the editing options work in the same way as when you’re editing Vertex subobjects. You can select multiple segments by holding down the Ctrl key while clicking the segments, or you can hold down the Alt key to remove selected segments from the selection set. You can also copy segments when they’re being transformed by holding down the Shift key. The cloned segments break away from the original spline, but are still a part of the Editable Spline object.

You can change segments from straight lines to curves by right-clicking the segment and selecting Line or Curve from the pop-up quadmenu. Line segments created with the Corner type vertex option cannot be changed to Curves, but lines created with Smooth or Bézier type vertex options can be switched back and forth.

Several Geometry rollout buttons work on more than one subobject type.

# Connect Copy

When you create a copy of a segment by moving a segment with the Shift key held down, you can enable the Connect Copy option to make segments that join the copied segment with its original. For example, if you have a single straight horizontal line segment, dragging it upward with the Copy Connect option enabled creates a copy that is joined to the original, resulting in a rectangle. Be aware that the vertices that connect to the original segment are not welded to the original segment.

# Divide

When you select a segment, the Divide button becomes active. This button adds the number of vertices specified to the selected segment or segments. These new vertices are positioned based on the curvature of the segment with more vertices being added to the areas of greater curvature. Figure 12.28 shows the diamond shape (second row, second from right) after all four segments were selected, a value of 1 was entered into the spinner, and the Divide button was clicked.

![](bbox=[0.067, 0.65, 0.405, 0.772])

# FIGURE 12.28

The Divide button adds segments to the spline.

# Detach

The Detach button separates the selected subobjects from the rest of the object (opposite of the Attach button). When you click this button, the Detach dialog box opens, enabling you to name the new detached subobject. When segments are detached, you can select the Same Shape option to keep them part of the original object. The Reorient option realigns the new detached subobject to match the position and orientation of the current active grid. The Copy option creates a new copy of the detached subobject.

You can use Detach on either selected Spline or Segment subobjects.