This does C = T * R. It is just as easy to write:

```
Matrix3x3f mat = Matrix3x3f.translate( tx, ty );
mat = Matrix3x3f.rotate( rad ).mul( mat );
```

This does C = R * T. But unless the matrix row/column order is specified, there is no way to understand that rotation happens before or after translation. This can be very confusing, so make sure you understand what is going on.

Changing from row major to column major doesn't just involve using a different rotation matrix. The order of vector * matrix is reversed. If row major is used, then the vector is a row, which is a 1 x 3 matrix. If column major is used, then the vector is a column, which is a 3 x 1 matrix. The row major is 1 x 3 * 3 x 3, but the column major is 3 x 3 * 3 x 1. I had to update the code to switch from column-major to row-major vector multiplication, and switch the order of the multiplication.

If all of the tutorials available were searched for rotation matrices, there would be some differences. Some libraries, tutorials, and documentation present the matrix transformations as row major, and some as column major. OpenGL, a very popular 3D graphics library, stores the matrix in memory as a single array of data, but some of the documentation shows the values in column-major format. I have seen numerous DirectX documents using row-major format.

# Note

> I remember when first learning about matrix rotation, I was reading tutorials on a website and I ran across a forum argument where two people were arguing about a rotation matrix. Each poster claimed the other one's minus sign was in the wrong place.

```
[cos(a), -sin(a), 0] [cos(a), sin(a), 0]
[sin(a), cos(a), 0] [-sin(a), cos(a), 0]
[ 0, 0, 1] [ 0, 0, 1]
```

Of course, both posters were correct—it was just that one was using a row-major notation, and the other using a column-major notation. You've been warned. :-)

Having discussed all the general problems that you'll face when first learning about all this stuff, I have glossed over the most complicated part—multiplying two matrices together. The next section presents the matrix class used for all the groovy math stuff (groovy is a technical term).

# UNDERSTANDING THE MATRIX3X3F CLASS

The code for adding and subtracting matrices is simple. The values for each index of the two matrices are added or subtracted from each other and placed into the same index. Only matrices of the same width and height can be added together, and you