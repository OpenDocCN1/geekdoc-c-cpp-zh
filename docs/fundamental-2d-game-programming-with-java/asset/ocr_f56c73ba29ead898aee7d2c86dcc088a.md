The vector (tx, ty, 1) is the translation vector and goes from the top to the bottom, occupying a column of the matrix.

The following transformation matrix is a row-major matrix:

```
[ 1 0 0 ]
[ 0 1 0 ]
[ tx ty 1 ]
```

Notice that the transformation vector now goes across the bottom, on the row.

Why is this important? The first reason is that the translation matrices have their values in different places, so mismatching them will cause errors. The second reason, as stated previously, is that M1 * M2 != M2 * M1. This means that order matters. This problem concerns order of operations.

Let C = a concatenation of matrices. If you scale (S), rotate (R), and translate (T), you end up with two different ways of writing the code.

```
C = S * R * T
C = T * R * S
```

Do you do it this way?

```
C = T.mul( R ).mul( S );
```

Or this way?

```
C = S.mul( R ).mul( T );
```

The answer is, either one is correct, depending on which matrix order is used. If the matrix is stored in row-major form, then matrix concatenation is done left to right. However, if column-major form is used, the matrix concatenation is performed from right to left. Remembering that M * N != N * M, you can see that it is very easy to get something in the wrong place, or do things in the wrong order.

# Note

> While writing the first version of this chapter, I didn't have much about row major and column major. After the first review, I realized that I had swapped some of the code. I was doing things for row major using column major. After fixing the errors, and re-testing everything, I added this section. :-)

To make it even more complicated, it is easy to write the following code:

```
Matrix3x3f mat = Matrix3x3f.translate( tx, ty );
mat = mat.mul( Matrix3x3f.rotate( rad ) );
```