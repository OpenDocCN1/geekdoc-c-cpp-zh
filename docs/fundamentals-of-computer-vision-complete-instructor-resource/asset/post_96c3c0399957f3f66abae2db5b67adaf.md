
- [12.27] K. Lee, Y. Choy, and S. Cho. Geometric structure analysis of document images: A knowledge-based approach. IEEE Trans. Pattern Anal. and Machine Intel., 22(11), 2000.
- [12.28] H. C. Longuet-Higgins. A computer algorithm for reconstructing a scene from two projections. Nature, September 1981.
- [12.29] J. Michel, N. Nandhakumar, and V. Velten. Thermophysical algebraic invariants from infrared imagery for object recognition. IEEE Trans. Pattern Anal. and Machine Intel., 19(1), January 1997.
- [12.30] F. Mokhtarian. Silhouette-based isolated object recognition through curvature scale space. IEEE Trans. Pattern Anal. and Machine Intel., 17(5), May 1995.
- [12.31] R. Morano, C. Ozturk, R. Conn, S. Dubin, S. Zietz, and J. Nissan. Structured light using pseudorandom codes. IEEE Trans. Pattern Anal. and Machine Intel., 20(3), March 1998.
- [12.32] S. Nayar and R. Bolle. Reflectance based object recognition. Int. J. of Computer Vision, 1996.
- [12.33] S. Nayar and Y. Nakagawa. Shape from focus. IEEE Trans. Pattern Anal. and Machine Intel., 16(8), August 1994.
- [12.34] M. Oren and S. Nayar. A theory of specular surface geometry. Int. J. of Computer Vision, 1996.
- [12.35] N. Page, W. Snyder, and S. Rajala. Turbine blade image processing system. In Proc. SPIE 0397. Applications of Digital Image Processing, volume 261, Oct 1983.
- [12.36] P. Rosen and G. West. Nonparametric segmentation of curves into various representations. IEEE Trans. Pattern Anal. and Machine Intel., 17(12), 1995.
- [12.37] H. Schultz. Retrieving shape information from multiple image of a specular surface. IEEE Trans. Pattern Anal. and Machine Intel., 16(2), February 1994.
- [12.38] H. Shum, I. Keuchci, and R. Reddy. Principal component analysis with missing data and its application to polyhedral object modeling. IEEE Trans. Pattern Anal. and Machine Intel., 17(9), 1995.
- [12.39] W. Snyder and G. Bilbro. Segmentation of range images. In Int. Conference on Robotics and Automation, March 1985.
- [12.40] B. Sroroka. Generalized cylinders from parallel slices. In Proceedings of the Conference on Pattern Recognition and Image Processing, 1979.
- [12.41] B. Sroroka and R. Bajcsy. Generalized cylinders from serial sections. In 3rd Int. Joint Conf. on Pattern Recognition, Nov 1976.
- [12.42] M. Soucy and D. Laurendeau. A general surface approach to the integration of a set of range views. IEEE Trans. Pattern Anal. and Machine Intel., 17(4), April 1995.
- [12.43] C. Stewart. Minipiran: A new robust estimator for computer vision. IEEE Trans. Pattern Anal. and Machine Intel., 17(10), 1995.
- [12.44] J. Stone and I. Isard. Adaptive scale filtering: A general method for obtaining shape from texture. IEEE Trans. Pattern Anal. and Machine Intel., 17(7), July 1995.
- [12.45] M. Subbarao and T. Choi. Accurate recovery of three-dimensional shape from image focus. IEEE Trans. Pattern Anal. and Machine Intel., 17(3), March 1995.
- [12.46] S. Sull and N. Ahuja. Integrated 3-d analysis and analysis-guided synthesis of flight image sequences. IEEE Trans. Pattern Anal. and Machine Intel., 16(4), April 1994.
- [12.47] S. Sullivan, L. Sandford, and J. Ponce. Using geometric distance fits for 3-d object modeling and recognition. IEEE Trans. Pattern Anal. and Machine Intel., 16(12), 1994.
- [12.48] Y. Sun, L. Liu, and J. Grady. Reconstruction of 3-d tree-like structures from three mutually orthogonal projections. IEEE Trans. Pattern Anal. and Machine Intel., 16(3), March 1994.
- [12.49] B. Super and A. Bovik. Shape from texture using local spectral moments. IEEE Trans. Pattern Anal. and Machine Intel., 17(4), April 1995.
- [12.50] K. Tarabanis, R. Tsai, and A. Kaul. Computing occlusion-free viewpoints. IEEE Trans. Pattern Anal. and Machine Intel., 18(3), March 1996.
- [12.51] G. Taubin. Nonplanar curve and surface estimation in 3-space. In IEEE Robotics and Automation Conference, May 1988.
- [12.52] P. Torr and D. Murray. The development and comparison of robust methods for estimating the fundamental matrix. International Journal of Computer Vision, 24(3), 1997.
- [12.53] E. Trucco and R. Fisher. Experiments in curvature-based segmentation of range data. IEEE Trans. Pattern Anal. and Machine Intel., 17(2), 1995.
- [12.54] R. Wang, A. Hanson, and E. Riseman. Fast extraction of ellipses. In Ninth International Conference on Pattern Recognition, 1988.
- [12.55] M. Wani and B. Batchelor. Edge-region-based segmentation of range images. IEEE Trans. Pattern Anal. and Machine Intel., 16(3), 1994.
- [12.56] I. Weiss and M. Ray. Model-based recognition of 3d objects from single images. IEEE Trans. Pattern Anal. and Machine Intel., 23(2), 2001.
- [12.57] R. Woodham. Photometric method for determining surface orientation from multiple images. Optical Engineering, 19, 1980.
- [12.58] Y. Lei and K. Wong. Ellipse detection based on symmetry. Pattern Recognition Letters, 20, 1999.
- [12.59] X. Yu, T. Bui, and A. Krzyzak. Robust estimation for range image segmentation and reconstruction. IEEE Trans. Pattern Anal. and Machine Intel., 16(5), 1994.
- [12.60] M. Zerroug and R. Nevatia. Three dimensional descriptions based on the analysis of the invariant and quasi-invariant properties of some curved-axis generalized cylinders. IEEE Trans. Pattern Anal. and Machine Intel., 18(3), March 1996.
- [12.61] R. Zhang, P. Tsai, J. Cryer, and M. Shah. Shape-from-shading: A survey. IEEE Trans. Pattern Anal. and Machine Intel., 21(8), Aug 1999.
- [12.62] J. Zheng. Acquiring 3-d models from sequences of contours. IEEE Trans. Pattern Anal. and Machine Intel., 16(2), February 1994.

## 13 Developing Computer Vision Algorithms

> Education is what remains after one has forgotten everything one learned in school.
> - Albert Einstein

We conclude the book with a look back in the context of how one develops good algorithms to solve Computer Vision problems. The steps are listed in order, as much as possible, with reference to materials and examples in the book.

The approach is explained through an example: Suppose you need to develop an algorithm to construct a panorama from two overlapping images. This requires that you find some way to transform coordinates in one image to appropriate coordinates in the next image, as described in Chapter 13.1. (See Figure 13.1.)

### Know the literature
If you are working on a problem that you think is important, chances are somebody else has also worked on it. Since the advent of Web searching, it has become easier to search, but don't limit your searches to Google. It's OK if you spend several days looking in the library. Looking at actual paper copies of old journal papers isn't necessarily a bad thing. After all, you plan to spend months or years on this project. Some papers were written before Web searching [13.2]. Often, you can be fortunate enough to find that someone else has done a good literature survey for you. For example, in the topic of the shape from motion, [13.3] and [13.1] thoroughly teach the relevant material.

### Form an Objective Function
In Chapter 6, we saw one example of finding an image that is the solution to an optimization problem. We found images that resembled the input image but also had some other desirable properties. In Chapter 5 we derived convolution kernels by finding best fits to data. In Chapter 12 objective functions were explicitly used twice.

In some rare instances, it isn't possible to set up a problem in terms of an optimization problem, but it's a good way to start.

### Do the Math Correctly
Once you have set up an objective function, you need to minimize it. For that, you often need a gradient. Can you find the gradient analytically as in section 6.5.1, or must you use numerical methods to estimate the gradient? In Chapter 12, we solved for a homography by using two images. But even if the math is correct, is it a valid approach? Can you even use this approach to solve general stereo problems? These questions are closely related to the next topic.

### Be Aware of Your Assumptions
Every semester we teach this course, we encounter students who think all images are composed of pixels with brightnesses that range
