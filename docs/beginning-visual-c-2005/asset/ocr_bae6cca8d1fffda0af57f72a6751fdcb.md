# Creating the Document and Improving the View

In this chapter, you’ll look into the facilities offered by MFC for managing collections of data items. You’ll use these to complete the class definition and implementation for the curve element that was left open in the last chapter. You’ll also extend the Sketcher application to store data in a document, and make the document view more flexible, introducing several new techniques in the process.

In this chapter, you’ll learn about:

+   - Collections and what you can do with them
+   - How to use a collection to store point data for a curve
+   - How to use a collection to store document data
+   - How to implement drawing a document
+   - How to implement scrolling in a view
+   - How to create a context menu at the cursor
+   - How to highlight the element nearest the cursor to provide feedback to the user for moving and deleting elements
+   - How to program the mouse to move and delete elements

# What Are Collection Classes?

By the nature of Windows programming, you’ll frequently need to handle collections of data items where you have no advance knowledge of how many items you will need to manage, or even what particular type they are going to be. This is clearly illustrated by the Sketcher application. The user can draw an arbitrary number of elements which can be lines, rectangles, circles and curves, and in any sequence. MFC provides a group of collection classes designed to handle