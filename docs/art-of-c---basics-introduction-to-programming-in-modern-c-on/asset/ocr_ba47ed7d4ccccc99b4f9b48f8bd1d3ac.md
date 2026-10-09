# Lesson 28. Rubik’s Cube

# 28.1. Problem

The Rubik’s Cube was wildly popular when it first came out in the 1970s. It is still very popular among the children, and among many enthusiasts and "speedcubers". Cf. [Rubik’s Cube](https://en.wikipedia.org/wiki/Rubik%27s_Cube).

This is a very interesting puzzle. Not very "complex", but it is still very difficult to visualize in mind. The space of all possible configurations of the Rubik’s Cube has a topology of $3$ dimensional $torus$ [https://en.wikipedia.org/wiki/Torus], as we will see shortly.

Now the question is, how to "represent" the configurations of the Rubik’s cube in a program? In particular, in this lesson, we will tackle a problem of "shuffling" a cube or randomizing its configurations.

Each side of the Rubik’s cube can be rotated by 90, 180, and 270 degrees. 180 and 270 degree rotations can be viewed as two and three 90 degree rotations, respectively. It is customary among the Rubik’s cube players, however, that counting 90 degree and 270 (-90) degree rotations as two distinct moves. A 180 degree rotation can still be viewed as two moves of one of these rotations.

The Rubik’s Cube has six sides or "faces" (it’s a cube after all), and hence, from any given configuration, we can make one of the 12 moves: A 90 degree clockwise or counterclockwise rotation for one of the 6 faces.

Each of the 6 faces is associated with a color, White (W), Blue (B), Red (R), Green (G), Orange (O), and Yellow (Y). The white and yellow faces are on the opposite sides of the cube. The blue and green faces are on the opposite sides. The red and orange faces are on the opposite sides.

It’s hard to represent a three-dimensional object on a two dimensional surface, but the Rubik’s cube can be drawn as follows: