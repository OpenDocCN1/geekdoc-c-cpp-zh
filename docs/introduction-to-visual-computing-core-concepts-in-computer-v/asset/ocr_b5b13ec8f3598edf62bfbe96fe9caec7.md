least eight correspondences to estimate $F$ using this method. In the subsequent sections we will see how $F$ is used for different purposes in different situations.

# 8.4 Essential Matrix

Essential matrix $E$ is defined as the fundamental matrix of normalized cameras. A normalized camera is achieved when the coordinates of the camera are normalized and hence the name. Therefore, the intrinsic matrix $K$ of a normalized camera is identity, i.e. $K = I$. Therefore, when considering two normalized correspondences $\hat{p}_1$ and $\hat{p}_2$, all the properties of fundamental matrix described in [Section 8.3.1](#) are now applicable to essential matrix, the most useful of them being

$$l_2 = E\hat{p}_1$$  \tag{8.42}

$$l_1 = E^T\hat{p}_2$$  \tag{8.43}

$$\hat{p}_2^T E\hat{p}_1 = 0$$  \tag{8.44}

$$\hat{p}_1^T E^T\hat{p}_2 = 0.$$  \tag{8.45}

The normalization removes two scale factors that denote the size of the pixel. Therefore, two degrees of freedom are reduced from $F$ to yield $E$. Hence, $E$ has five degrees of freedom.

Since any pair of camera can be reduced to the situation where $C_1$ is aligned with the world coordinate axes and $C_2$ translated by $T$ and rotated by $R$ with respect to $C_1$, we derive the essential matrix $E$ by replacing $K_1 = K_2 = I$ in [Equation 8.34](#) giving

$$E = [T]_X R$$  \tag{8.46}

Since $R$ and $[T]_X$ are both symmetric matrices, we can find $E^T$ as

$$E^T = ([T]_X R)^T = R^T[T]_X^T = R[T]_X$$  \tag{8.47}

The five degrees of freedom of $E$ can also be seen from the above equations. Since $E$ depends on $R$ and $T$ that have two and three degrees of freedom respectively, $E$ has five degrees of freedom.

# 8.5 Rectification

Rectification is a process by which we take the images from a pair of stereo cameras and apply appropriate transformations such that they simulate the case of the frontal eyes and therefore the correspondences lie on the raster lines. In this section we will learn how to rectify images from two normalized uncalibrated cameras.