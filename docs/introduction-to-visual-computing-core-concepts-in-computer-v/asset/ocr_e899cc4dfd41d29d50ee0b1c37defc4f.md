# Exercises

+   1. Why is the epipolar constraint useful for stereo matching (i.e. finding corresponding points between the first and the second images)? What happens to the epipoles and the epipolar lines in the rectified images after applying image rectification? What are the advantages of applying image rectification before we do stereo matching?

+   2. Given a point $p=(x,y)$ in image 1, and the fundamental matrix

$$F=\begin{pmatrix}0&1&0\\1&0&-1\\0&1&0\end{pmatrix}\qquad (8.67)$$

+   (a) Derive the equation of the corresponding epipolar line in image 2. Use your result to compute the equations of the epipolar lines corresponding to the points $(2,1)$ and $(-1,-1)$.

+   (b) Compute the epipole of image 2 using the equation of the two lines you derived for the previous question. In general, how can you determine the epipole from any fundamental matrix $F$? (Hint: the answer involves a term from linear algebra.)

+   (c) The relationship between points in the second image and their corresponding epipolar lines in the first image is described by the transpose of the fundamental matrix $F^T$. Use this fact to compute the epipole in image 1 for the matrix $F$.

+   (d) Which of the following points is the epipole of the first camera? (i) $(0.5,0.5)$; (ii) $(1,1)$; (iii) $(1,0)$ and (iv) $(-1,0)$.

+   (e) Which of the following points is the epipole of the second camera? (i) $(0.5,0.5)$; (ii) $(1,1)$; (iii) $(1,0)$ and (iv) $(-1,0)$.

+   (f) Consider the point $(0.5,0.5)$ in the first camera. Find the slope and offset of the epipolar line in the second camera on which its correspondence will lie.

+   (g) Let the two cameras have the focal lengths of 1 and 2 respectively with square pixels, principal center at the center of the image plane and no skew factor. Find the essential matrix that relates these two cameras.

+   3. Consider a pair of camera stereo rig whose rotation and translation with respect to global coordinate system is $R_1$, $R_2$, $T_1$ and $T_2$ respectively. Their intrinsic matrix is identity. Give an expression of the essential matrix and the length of the baseline in terms of these matrices.