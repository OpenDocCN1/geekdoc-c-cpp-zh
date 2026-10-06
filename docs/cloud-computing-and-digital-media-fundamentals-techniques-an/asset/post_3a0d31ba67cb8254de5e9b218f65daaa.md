
# Research on Scene 3D Reconstruction ■ 261

independence, and so on, which will benefit the scene reconstruction pipeline a lot.

In this section, there are two fundamental research goals:

- 1. Describe the scene reconstruction pipeline in detail.
- 2. Discuss our research on applying scene reconstruction on cloud computing platform.

## 11.2 SCENE RECONSTRUCTION PIPELINE

The scene reconstruction pipeline takes an unordered collection of images (for instance, from the Internet search or a personal collection) and produces 3D camera and scene geometry. In particular, for each input photo, the pipeline determines the location from which the photo was taken and the direction in which the camera was pointed, and recovers the 3D coordinates of a sparse set of points in the scene.

The basic principles behind recovering geometry from a set of images are fairly simple. Humans implicitly use multiview geometry to sense depth with binocular vision. If we see the same point in the world with both eyes, we can implicitly "triangulate" to determine its rough distance. Similarly, given two photographs of the same scene, a list of pixels in images A and B, and the relative poses of the cameras used to capture the images, the 3D position of the matching pixels can be calculated. However, even though we can get the corresponding pixels by comparing a pair of images, the geometry of cameras that took these two often keeps unknown. In another word, only if we determine that the camera poses according to the matching pixels as well, we can construct the structure of the scene geometry successfully. Fortunately, the correspondences place constraints on the physical configuration of the two cameras. Thus, given enough point matches between two images, the geometry of the system becomes constrained enough that we can determine the two-view geometry, after which we can estimate the 3D point positions using triangulation. This procedure is also known as SfM. In general, SfM can deal with an arbitrary number of images and correspondences, and estimate camera and point geometry simultaneously.

### 11.2.1 SIFT Algorithm

SIFT is an algorithm in computer vision to detect and describe local features in images. To begin with, SIFT extracts features from a set of reference images and stores them into a database. An object is recognized in a new image by individually comparing each feature from the new image to this database and finding candidate matching features based on the Euclidean distance of their feature vectors. Since SIFT feature descriptor is invariant to scale, orientation, and affine distortion, and partially invariant to illumination changes, this method can robustly identify objects even among clutter and under partial occlusion. It has wide applications, such as object recognition, robotic popping and navigation, image stitching, 3D modeling, gesture recognition, video tracking, and match moving.

In scene reconstruction, the pipeline uses SIFT to detect the key features of images for the initial matching. There are five main steps in SIFT listed below:

- 1. Scale-space extrema detection
- 2. Accurate keypoint localization
- 3. Orientation assignment
- 4. Compute local image descriptor
- 5. Keypoint matching

#### 11.2.1.1 Scale-Space Extrema Detection

To apply SIFT, transformation of the format of input image is necessary. In general, we change the input image into gray scale. Also, to make full use of the input, the image can be expanded to create more sample points than presented in the original.

The most important goal of SIFT is to achieve invariance. In order to attain invariance, theoretically, we need to search stable features in all possible scales. But in practice, it is impossible to get all scales, here we sample the scale space for reasonable frequency to attain invariant feature detection. In SIFT, difference of Gaussian (DoG) filter is used to build up the scale space [3]. DoG: (1) it is an efficient filter and (2) it provides a close approximation to scale-normalized Laplacian of Gaussian. The normalization of the Laplacian with the factor $s^2$ is required for true invariance. In SIFT, the author proved that DoG scale space will be almost the same as that of Laplacian Gaussian (Figure 11.3).

![](img/f13da3dd59d15874e4b22b03a274001b_285_0.png)

FIGURE 11.3 DoG and Gaussian pyramids. DoG, difference of Gaussian. From David G. Lowe, International Journal of Computer Vision, 60, 99–110, 2004. With permission.)

It is very simple to get DOG filter; we only need to subtract images convoluted with Gaussian low-pass filter in different scales. Also, since we have preprocessed the input image to prevent significant aliasing, we need to make sure that the blurring factor s is above threshold T.

The final step of extrema detection is to compare each pixel with its neighbors: 8 neighbors in its current scale level and 18 neighbors in its nearest neighbors. Only if the pixel is bigger than all of its neighbors, it will be chosen as a keypoint candidate.

#### 11.2.1.2 Accurate Keypoint Localization

In the previous step, we have found out the possible feature points. Then, we must eliminate extrema that are along the edges but are unstable by small amounts of noise because of poorly determined position. According to the scale-space value, we can first remove the points that are near to the boundary. Second, we eliminate poorly defined peaks in the DoG function which have a large principal curvature across the edge but a small one in the perpendicular direction.

#### 11.2.1.3 Orientation Assignment

By assigning a consistent orientation to each keypoint based on local properties, this descriptor can be represented yet therefore invariant to rotation. In SIFT, the orientation histogram is used to determine major orientation.

![](img/f13da3dd59d15874e4b22b03a274001b_286_0.png)

FIGURE 11.4 The orientation assignment. First, we compute the histogram in a window whose center is keypoint and then we divide it into 36 bins. Each sample added to the histogram is weighted by Gaussian function. The angle of the longest bin is referred as the orientation. Therefore, for robustness, if the other bins are over 80% of the longest bin, they will be treated as inliers (Figure 11.5).

#### 11.2.1.4 Local Image Descriptor

This step of SIFT is to generate local descriptor that is highly distinctive yet as invariant as possible to remaining variations, such as change in illumination or viewpoint. To begin with, SIFT computes 16 × 16 window using much fewer degree of 8. It subdivides the window into 4 × 4 subwindows and recompute the weights of each orientation and produce a 4 × 4 × 8 descriptor.

![](img/f13da3dd59d15874e4b22b03a274001b_287_0.png)

FIGURE 11.5 Local image descriptor.

#### 11.2.1.5 Keypoint Matching

To determine an inlier of matched keypoints, we should find the nearest neighbor and the second nearest neighbor of each point. The nearest neighbor is defined as the keypoint with minimum Euclidean distance for the invariant descriptor. For robustness, SIFT uses the ratio of the nearest neighbor to the second nearest neighbor, $d_1/d_2$ of 0.6 to determine whether the matches are inliers.

Approximate nearest neighbor (ANN) searching algorithm [6] is a library written in C++, which supports data structures and algorithms for both exact and ANN searching in arbitrarily high dimensions. However, computing the exact nearest neighbors in dimensions much higher than 8 seems to be a very difficult task. Few methods seem to be significantly better than a brute force computation of all distances. To improve the efficiency

## 11.2.2 RANSAC Paradigm

In this section, we introduce the RANSAC paradigm, which is capable of smoothing data that contain a significant percentage of gross errors. SIFT, the local feature detector, always makes mistakes, as described in Section 11.2.1, although it is one of the best local feature detectors. There are two kinds of mistakes: classification errors and measurement errors. Classification errors occur when a feature detector incorrectly identifies a portion of an image as an occurrence of a feature, whereas measurement errors occur when the feature detector correctly identifies the feature, but slightly miscalculates one of its parameters (e.g., its location in the image). To get rid of noise data from images and refine
