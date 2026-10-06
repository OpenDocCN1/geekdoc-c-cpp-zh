baseline (distance between camera centers), so that the initial two-frame reconstruction can be robustly estimated. Since homography matrix H represents the transformation between two images of a single plane or two images taken at the same location (possibly with different direction). Thus, if a homography cannot fit to the correspondences between two images, it indicates that the cameras have some distance between them, and that is what we want.

In Section 11.2.3, homography matrix between each pair of matching images is created and the percentage of feature matches are inliers to the estimated homography. Then a pair of images that have the lowest percentage of inliers, but have at least threshold over matches, will be chosen as initial image pair.

The system estimates the extrinsic parameters for the initial pair using five-point algorithm [7], and then tracks visible in the two images are agitated, giving an initial set of 3D points.

# 11.2.5.1 Recovering Camera Geometry

In Section 11.2.3, we have examined the properties of F and image relations for point correspondence x'. We now turn to one of the most significant properties of F that may be used to determine the camera matrices of the two views.

11.2.5.1.1 The Essential Matrix To compute the extrinsic parameters of camera, the conception of essential matrix to extract extrinsic parameters should be introduced first. The essential matrix is the specialization of the fundamental matrix to the case of normalized image. Historically, the essential matrix was introduced before the fundamental matrix, and the fundamental matrix may be thought of as the generalization of the essential matrix in which the (inessential) assumption of calibrated cameras is removed. The essential matrix has fewer degrees of freedom, and additional properties, compared to the fundamental matrix. These properties are described below.

Consider a camera matrix decomposed as P = K [R t], and let x=PX be a point in the image. If the calibration matrix K is known, then we may apply its inverse to the point x to obtain the point. Then we have x=[R t]X, where x is the image point expressed in normalized coordinates. It may be thought of as the image of the image X with respect to a camera [R t] having the identity matrix I as calibration matrix.