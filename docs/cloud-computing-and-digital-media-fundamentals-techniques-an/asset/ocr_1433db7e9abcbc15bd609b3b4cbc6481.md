# Research on Scene 3D Reconstruction ■ 279

SVD of A. Then unit singular vector corresponding to the smallest singular value is the solution X.

# 11.2.6 Adding New 3D Points and Cameras

In Section 11.2.5, we successfully constructed the initial pair of camera matrices and initial 3D points. Then we will add more cameras and points by turn. Cameras that observe the threshold over the number of tracks whose 3D locations have already been estimated will be selected. To initialize the pose of the new camera, for each correspondence $X_i \neq$ x_i$, we derive a relationship:

```
$$\begin{matrix} \hat{E} & 0^T & -w_iX_i^T & y_iX_i^T\hat{P}^1^T = \ \w_ix_i^T & 0^T & -x_ix_i^T & \hat{P}^2^T =0 \ \y_ix_i^T & x_ix_i^T & 0^T & \hat{P}^3^T = \end{matrix} (11.18)$
```

Where $P^i$ is a four-vector, the $i$th row of $P$, where $i=1, 2, 3, \dots$— Only two of the equations are linear independent. Since the matrix $P$ has 12 entries and 11 degrees of freedom, it is necessary to have 11 equations to solve for $P$. We need to combine six-point correspondence to form the $Ap=0$, where $A$ is an $11 \times 12$ matrix in this case. In general, a $A$ will have rank 11, and the solution vector $p$ is the 1D right null space of $A$. Of course, there exists noise in the correspondences; the DLT is applied again to compute the optimal $P$ for the selected points. Moreover, since we cannot select the best six points to compute the optimal $P$, we apply RANSAC paradigm to help us select the best $P$ among possible candidates.

Then we add points observed by the new camera into the reconstruction. A point is added if it is observed by at least two cameras, and triangulating the points gives a well-conditioned estimate of its location. Once the new points have been added, sparse bundle adjustment (SBA) [9] is performed on the entire model.

This procedure of initializing cameras, triangulating points, and SBA is repeated, until no remaining camera observes a sufficient number of points (in Reference 1, at least 20). In general, not all images will be reconstructed. The reconstructed images are not selected by human work, but are determined by the algorithm as it adds until no more reliably be added.