Equation 12.30 may be solved for f using singular valued decomposition (SVD) (see section 3.2.9). SVD will find three matrices, U, D, and V, such that A = UDV^T. The column of V corresponding to the smallest singular value will be the least-squares estimate of f. F is then reconstructed from f using Eq. 12.27.

One problem remains: it is very important that F be singular; specifically of rank 2. Again use SVD, writing F = UDV^T, and D will be diagonal with the three singular values on the diagonal,

$$ F = U \begin{bmatrix} D_{11} & 0 & 0 \\ 0 & D_{22} & 0 \\ 0 & 0 & D_{33} \end{bmatrix} V^T. $$

Depending on the implementation, the smallest singular value will be either D11 or D33. We need to set the smallest one to zero. Assume for now that the smallest singular value is D33.

The rank 2 diagonal matrix closest D will be

$$ D' = \begin{bmatrix} D_{11} & 0 & 0 \\ 0 & D_{22} & 0 \\ 0 & 0 & 0 \end{bmatrix}. $$

The new estimate of F is then constructed from

$$ F = UDV^T \qquad (12.31) $$

and this estimate will have rank 2, as required.

So, given correspondences, it is possible to eliminate erroneous correspondences and find the fundamental matrix. In the next section, we find the camera matrices from F.

# ## 12.3.3 Finding the Camera Matrices

You could try getting out your tape measure and your protractor and measuring the position and orientation of the two cameras. In principle, you could find the camera matrices in that way. But, let's think about that: Let's say your digital camera has a 1000 x 1000 array of pixels on a 1cm x 1cm chip, which means your pixels are spaced ten microns apart. A measurement error of ten microns displaces your camera origin by one pixel. Exactly how accurately IS your tape measure? Instead of measuring, we can use the camera itself to figure out the camera matrices.

In section 12.3.1 you learned how to find the fundamental matrix. This subsection presents one way to find the two camera matrices from the fundamental matrix.

Given a fundamental matrix F, the two camera matrices may be chosen to be

$$ P_l = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{bmatrix} \text{ and } P_r = [[e']_\times F | e']. \qquad (12.32) $$

Here e' is the epipole satisfying e'^T F = 0.