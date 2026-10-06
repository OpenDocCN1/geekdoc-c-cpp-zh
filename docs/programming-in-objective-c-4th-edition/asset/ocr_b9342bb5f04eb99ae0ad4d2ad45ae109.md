having to constantly add new definitions to the same interface and implementation files. This is particularly handy when you want to do this to a class for which you don't have access to the source code. You'll learn about categories in Chapter 11, "Categories and Protocols."

# A Point Class and Object Allocation

The Rectangle class stores only the rectangle's dimensions. In a real-world graphical application, you might need to keep track of all sorts of additional information, such as the rectangle's fill color, line color, location (origin) inside a window, and so on. You can easily extend your class to this. For now, let's deal with the idea of the rectangle's "origin" means the location of the rectangle's lower-left corner within some Cartesian coordinate system (x, y). If you were writing a drawing application, this point might represent the location of the rectangle inside a window, as depicted in Figure 8.4.

# Figure 8.4. A rectangle drawn in a window

![](bbox=[0.267, 0.606, 0.732, 0.831])

In Figure 8.4, the rectangle's origin is shown at (x1, y1).