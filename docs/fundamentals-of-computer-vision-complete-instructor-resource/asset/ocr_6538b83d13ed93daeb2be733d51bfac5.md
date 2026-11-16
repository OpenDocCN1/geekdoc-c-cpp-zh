![](bbox=[0.196, 0.116, 0.508, 0.292])

Figure 12.8 The right-hand image of a pair of images containing one pair of possibly corresponding points: x in the left image and x_r in the right. The line l_r is the set of all points in the right image that could correspond to x. If the correspondence were perfect, x_r would lie on this line. Therefore the distance d(x_r, l_r) is a measure of the possible error in this proposed correspondence.

+   (b) Find the epipolar line distances, illustrated in Figure 12.8. This distance may be found by \( d(x_r, l_r) = \frac{|ax_r|}{(a^2+b^2)^{1/2}} \) in the left image, and similarly in the right. (Remember that l is the vector \( [a \ b \ c]^T \), the coefficients of the equation \( ax + by + c = 0 \)).

+   (c) Compute an error

\( E = d(x_r, L_r) + d(x_r, L_r). \) (12.23)

+   (d) If E is too large, it is an outlier, otherwise it is an inlier. Therefore a threshold will be needed. Many applications choose a maximum distance of 1 pixel.

+   4. At iteration k, the estimate of F just found in the previous step is denoted F_k. Test this value of F over all the proposed correspondences in S_r and keep track that all the correspondences that are consistent with F_k. We will call this the inlier set that has cardinality |S_k|. If |S_k| is the largest seen so far, store the fact that F_k is the best seen so far. That is, F_k explains more of the inlier correspondences.

+   5. Randomly choose another 8 points and find another possible F, repeating the steps above until some maximum, N, iterations have been run, or we have found a single F that has all the correspondences in its inlier set.

The algorithm above is a particular version of a very general method, Random Sample Consensus (RANSAC) [12.8, 12.52] for finding models in the presence of noise that may contain outliers. It is perhaps easiest to see the concept of an outlier in the context of determining if a point is from a particular Gaussian probability distribution: if the point is more than three standard deviations away from the mean, we would typically call that point an outlier. In this application, we do not use a probabilistic model, but the philosophy is the same.

And yes, we still haven't told you how to find the 3D position in space.

# 12.3.2 The 8-Point Algorithm

Before we continue, we should discuss the range of the numbers being dealt with. Using pixel coordinates, typical images have coordinates between 0 and around 1000. Algorithms