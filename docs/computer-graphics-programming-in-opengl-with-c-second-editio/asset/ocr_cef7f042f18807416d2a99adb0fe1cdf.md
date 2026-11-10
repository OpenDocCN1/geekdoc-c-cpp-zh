location to another. In this chapter, we will learn several useful transformation matrices:

+   - *Translation*
+   - *Rotation*
+   - *Scale*
+   - *Projection*
+   - *Look-At*

An important property of our transformation matrices is that they are all of size 4x4. This is made possible by our decision to use the *homogeneous* notation. Otherwise, some of the transforms would be of diverse and incompatible dimensions. As we have seen, ensuring they are the same size is not just for convenience; it also makes it possible to combine them arbitrarily, and pre-compute groups of transforms for improved performance.

# 3.4.1 Translation

A *translation* matrix is used to move items from one location to another. It consists of an identity matrix, with the X, Y, and Z movement(s) given in locations A₀₃, A₁₃, A₂₃. Figure 3.3 shows the form of a translation matrix and its effect when multiplied by a homogeneous point; the result is a new point “moved” by the translate values.

![](bbox=[0.347, 0.624, 0.653, 0.737])

Note that point (X,Y,Z) is translated (or moved) to location (X+Tₓ, Y+Tᵧ, Z+T𝓏) as a result of being multiplied by the translation matrix. Also note that multiplication is specified *right to left*.

For example, if we wish to move a group of points upward 5 units along the positive Y direction, we could build a translation matrix by taking an identity matrix and placing the value 5 in the Tᵧ position. Then we simply multiply each of the points we wish to move by the matrix.