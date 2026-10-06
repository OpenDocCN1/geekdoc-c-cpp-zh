# Research on Scene 3D Reconstruction ■ 261

independence, and so on, which will benefit the scene reconstruction pipeline a lot.

In this section, there are two fundamental research goals:

+   1. Describe the scene reconstruction pipeline in detail.

+   2. Discuss our research on applying scene reconstruction on cloud
computing platform.

# 11.2 SCENE RECONSTRUCTION PIPELINE

The scene reconstruction pipeline takes an unordered collection of images
(for instance, from the Internet search or a personal collection) and pro-\uces 3D camera and scene geometry. In particular, for each input photo,
the pipeline determines the location from which the photo was taken and the direction in which the camera was pointed, and recovers the 3D coord-\dinates of a sparse set of points in the scene.

The basic principles behind recovering geometry from a set of images
are fairly simple. Humans implicitly use multiview geometry to sense\depth with binomial vision. If we see the same point in the world with both
eyes, we can implicitly "triangulate" to determine its rough
distance. Similarly, given two photographs of the same scene, a list of
pixels in images A and B, and the relative poses of the cameras used to
capture the images, the 3D position of the matching pixels can be cal-\culated. However, even though we can get the corresponding pixels by
comparing a pair of images, the geometry of cameras that took these two
 often keeps unknown. In another word, only if we determine that
the camera poses according to the matching pixels as well, we can con-\struct the structure of the scene geometry successfully. Fortunately, the
correspondences place constraints on the physical configuration of the
two cameras. Thus, given enough point matches between two images, the
geometry of the system becomes constrained enough that we can deter-\mine the two-view geometry, after which we can estimate the 3D point
positions using triangulation. This procedure is also known as SfM.
in general, SfM can deal with an arbitrary number of images and corre-
spondences, and estimate camera and point geometry simultaneously.

# 11.2.1 SIFT Algorithm

SIFT is an algorithm in computer vision to detect and describe local
features in images. To begin with, SIFT extracts features from a set of