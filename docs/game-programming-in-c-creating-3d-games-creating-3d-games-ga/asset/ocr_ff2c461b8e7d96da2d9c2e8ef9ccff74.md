they maintain the coplanar property.

2D games use triangles to represent sprites by drawing a rectangle and filling in the rectangle with colors from an image file. We discuss this in much greater detail later in the chapter.

# Normalized Device Coordinates

To draw a triangle, you must specify the coordinates of its three vertices. Recall that in SDL, the top-left corner of the screen is (o, o), positive x is to the right, and positive y is down. More generally, a **coordinate space** specifies where the origin is and in which direction its coordinates increase. The **basis vectors** of the coordinate space are the direction in which the coordinates increase.

An example of a coordinate space from basic geometry is a **Cartesian coordinate system** (see Figure 5.1). In a 2D Cartesian coordinate system, the origin (o, o) has a specific point (usually the center), positive x is to the right, and positive y is up.