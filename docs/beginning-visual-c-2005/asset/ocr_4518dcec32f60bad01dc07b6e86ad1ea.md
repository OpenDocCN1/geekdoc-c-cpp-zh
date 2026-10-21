# Chapter 15

You have improved the view capability in Sketcher in several ways. You’ve added scrolling to the views using the MFC class CScrollView, and you’ve introduced a pop-up at the cursor for moving and deleting elements. You have also implemented an element highlighting feature to provide the user with feedback when moving or deleting elements.

You have covered quite a lot of ground in this chapter, and some of the important points you need to keep in mind are:

+   - If you need a collection class to manage your objects or pointers, the best choice is one of the template-based collection classes because they provide type-safe operation in most cases.
+   - When you draw in a device context, coordinates are in logical units that depend on the mapping mode set. Points in a window that are supplied along with Windows mouse messages are in client coordinates. The two coordinate systems are usually not the same.
+   - Coordinates that define the position of the cursor are in screen coordinates that are measured in pixels relative to the upper- left corner of the screen.
+   - Functions to convert between client coordinates and logical coordinates are available in the CDC class.
+   - Windows requests that a view is redrawn by sending a WM_PAINT message to your application. This causes the OnDraw() member of the affected view to be called.
+   - You should always do any permanent drawing of a document in the OnDraw() member of the view class. This ensures that the window is drawn properly when required by Windows.
+   - You can make your OnDraw() implementation more efficient by calling the RectVisible() member of the CDC class to check whether an entity needs to be drawn.
+   - To get multiple views updated when you change the document contents, you can call the UpdateAllViews() member of the document object. This causes the OnUpdate() member of each view to be called.
+   - You can pass information to the UpdateAllViews() function to indicate which area in the view needs to be redrawn. This makes redrawing the views faster.
+   - You can display a context menu at the cursor position in response to a right mouse click. This menu is created as a normal pop-up.

# Exercises

You can download the source code for the examples in the book and the solutions to the following exercises from http://www.wrox.com.

+   1. Implement the CCurve class so that points are added to the head of the list instead of the tail.
+   2. Implement the CCurve class in the Sketcher program using a typed pointer list, instead of a list of objects to represent a curve.
+   3. Look up the CArray template collection class in Help, and use it to store points in the CCurve class in the Sketcher program.