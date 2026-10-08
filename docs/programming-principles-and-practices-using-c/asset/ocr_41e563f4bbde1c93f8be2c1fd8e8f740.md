+   20. What properties can you set for a text string in a **Text**?
21. What is a font and why do we care?
22. What is **Vector_ref** for and how do we use it?
23. What is the difference between a **Circle** and an **Ellipse**?
24. What happens if you try to display an **Image** given a file name that doesn’t refer to a file containing an image?
25. How do you display part of an image?

# Terms

+   closed shape
color
ellipse
fill
font
font size
GIF
image
image encoding
invisible
JPEG
line
line style
open shape
point
polygon
polyline
unnamed object
**Vector_ref**
visible

# Exercises

For each “define a class” exercise, display a couple of objects of the class to demonstrate that they work.

+   1. Define a class **Arc**, which draws a part of an ellipse. Hint: `fl.arc()`.
2. Draw a box with rounded corners. Define a class **Box**, consisting of four lines and four arcs.
3. Define a class **Arrow**, which draws a line with an arrowhead.
4. Define functions **n()**, **s()**, **e()**, **w()**, **center()**, **ne()**, **se()**, **sw()**, and **nw()**. Each takes a **Rectangle** argument and returns a **Point**. These functions define “connection points” on and in the rectangle. For example, **nw(r)** is the northwest (top left) corner of a **Rectangle** called **r**.
5. Define the functions from exercise 4 for a **Circle** and an **Ellipse**. Place the connection points on or outside the shape but not outside the bounding rectangle.
6. Write a program that draws a class diagram like the one in §12.6. It will simplify matters if you start by defining a **Box** class that is a rectangle with a text label.
7. Make an RGB color chart (e.g., search the web for “RGB color chart”).
8. Define a class **Regular_hexagon** (a regular hexagon is a six-sided polygon with all sides of equal length). Use the center and the distance from the center to a corner point as constructor arguments.
9. Tile a part of a window with **Regular_hexagons** (use at least eight hexagons).