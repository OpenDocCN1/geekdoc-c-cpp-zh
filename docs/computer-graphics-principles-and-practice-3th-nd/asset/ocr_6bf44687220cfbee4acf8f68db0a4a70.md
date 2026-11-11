method of rendering. Through this, we hope you'll gain insight into the ways we represent the real world in computer graphics. We start with a discussion of visibility.

# ## 3.2 Visibility

The matter of selecting only visible points might not even have occurred to Dürer, but it is important for us. One way for Dürer to determine whether a point P is visible is to place the pointer on P and see whether the string runs in a straight line to the screw eye, or has to bend around some other part of the lute or other object to get there. In making our simplified model of the process, we'll disregard the issue of visibility determination, for the time being, not because it's unimportant—Chapter 36 is entirely about data structures for improving visibility computations—but because it is both tricky in general and unnecessary for the model we'll be drawing in this simple renderer.

# ## 3.3 Implementation

To mimic the woodcut's algorithm, we'll use algebra and geometry, and a very simple description of a very simple shape: We'll describe a cube by giving the locations of its six corners (or vertices), and by noting which pairs of vertices are connected by an edge. Thus, our model of a cube can be considered a wire-frame model, in which an object is created by connecting pieces of wire together.

To make the geometry simple, we'll establish a particularly nice way of measuring coordinates in the room. The origin of our coordinate system (see Figure 3.3) will be at the screw eye on the wall, and will be denoted E (for “eye”). The drawing frame will be in the z = 1 plane (i.e., we measure the distance from the screw eye to the plane of the drawing frame, and choose a system of units in which this distance is 1). The point on this plane that's closest to the screw eye will be called T; its coordinates are (0, 0, 1). We'll make the y-axis vertical and the x-axis horizontal, as shown.

The frame, within the z = 1 plane, will extend from the point (x_min, y_min, 1) to the point (x_max, y_max, 1), where x_min < x_max and y_min < y_max, as the names suggest, and where, for simplicity and consistency with the drawing (in which the frame appears fairly square^1), we'll assume that the width, x_max − x_min, is the same as the height, y_max − y_min. To be precise, two opposite corners of the frame are points whose 3D coordinates are (x_min, y_min, 1) and (x_max, y_max, 1).

**Inline Exercise 3.3:** What are the coordinates of the other two corners of the frame?

We'll also imagine that the paper that fills the frame (when the shutter is closed) is actually graph paper, whose lower-left corner is labeled (x_min, y_min) and whose upper-right corner is labeled (x_max, y_max), therefore providing us with

1. The panel that fills the frame does not appear square, however; we'll stick with squareness for simplicity.