# # 12.4 Image Stitching and Homographies

This section discusses *homographies* that map between points in two images. The coordinate representation used is *homogeneous coordinates*. That is, let a point in image 1 be \(\begin{bmatrix} x \ y \ 1 \end{bmatrix}\), and suppose the corresponding point in image 2 is \(\begin{bmatrix} x' \ y' \ 1 \end{bmatrix}\). Then the 3 x 3 matrix \(H\) will have the property that

```
\(\begin{bmatrix} w'x' \ w'y' \ w' \end{bmatrix} = H \begin{bmatrix} x \ y \ 1 \end{bmatrix}.\) (12.41)
```

From \(\begin{bmatrix} w'x' \ w'y' \ w' \end{bmatrix}\), one can find the point on the focal plane by dividing by the third coordinate, \(w'\).

Expanding the previous equation, we find

```
\(\begin{bmatrix} wx' \ wy' \ w' \end{bmatrix} = \begin{bmatrix} h_{11}x + h_{12}y + h_{13}w \ h_{21}x + h_{22}y + h_{23}w \ h_{31}x + h_{32}y + h_{33}w \end{bmatrix}.\) (12.42)
```

Since these are homogeneous representations of vectors, they represent projective operations.

As you follow the derivation of \(H\), you will find that the process of finding homographies is similar to that of finding the fundamental matrix. Both are based on finding correspondences, and make use of the cross product. Rather than simply pointing out the differences from finding \(F\), the derivation for finding \(H\) is presented in complete form here.

The algorithm needs as many correspondences as possible (the more you find, the better it will work ... at least ten) between the two pictures. Obviously these must be in the overlapped area of the two images.

Given a correspondence, \(\mathbf{x}' = H\mathbf{x}\), we make use of the same observation that we did in section 12.3.4, that if two vectors are equal, their cross product is zero.

Given two vectors, \(\mathbf{u}\) and \(\mathbf{v}\), the first element of the cross product is \(u_2v_3 - u_3v_2\), and in this problem

```
\(\mathbf{u} = \begin{bmatrix} wx' \ wy' \ w' \end{bmatrix} \quad \mathbf{v} = \begin{bmatrix} h_{11}x + h_{12}y + h_{13}w \ h_{21}x + h_{22}y + h_{23}w \ h_{31}x + h_{32}y + h_{33}w \end{bmatrix}\) (12.43)
```

and the first element of the cross product becomes

```
\(c_1 = u_2v_3 - u_3v_2 = y'(h_{31}x + h_{32}y + h_{33}w) - w'(h_{21}x + h_{22}y + h_{23}w)\) (12.44)
```

Since we need to write \(H\) as a vector, \(\mathbf{h}\), define \(h_1 = h_{11}, h_2 = h_{12}, h_3 = h_{13}, h_4 = h_{21}, \dots h_9 = h_{33}\), and then sort the terms of Eq. 12.44 by the subscript on \(h\), so that we