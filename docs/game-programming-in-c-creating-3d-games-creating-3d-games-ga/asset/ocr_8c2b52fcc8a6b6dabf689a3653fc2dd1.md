directly to the left or right; the direction doesn’t matter for the purposes of the intersection test. In 2D, this is as follows:

\(\widehat{n} = \langle 1, 0 \rangle\)

Because the min point for the box is on its left plane, the \( d \) value is as follows:

\( d = -P \cdot \widehat{n} = -min \cdot \langle 1, 0 \rangle = -min_x \)

Similarly, the dot products in the segment versus plane intersection equation also simplify to their x components. This means the final equation solving for intersection against the left plane is as follows:

\( t = \frac{-Start \cdot \langle 1, 0 \rangle - d}{(End - Start) \cdot \langle 1, 0 \rangle} = \frac{-Start_x - (-min_x)}{End_x - Start_x} = \frac{Start_x + min_x}{End_x - Start_x} \)

The equations for the other side planes have similar derivations. For 3D, there are a total of six planes to test. Listing 10.7 shows a helper function that encapsulates the behavior of testing a single side plane. Note that if the segment intersects with the plane, the function adds the \( t \) value to a supplied `std::vector`. The intersection function uses this `std::vector` to test all possible \( t \) values in order, from earliest to latest planar intersection.

# Listing 10.7 Line Segment Versus AABB Helper Function