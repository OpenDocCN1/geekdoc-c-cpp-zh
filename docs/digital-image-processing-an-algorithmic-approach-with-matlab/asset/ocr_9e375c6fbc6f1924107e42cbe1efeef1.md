![](bbox=[0.06, 0.08, 0.91, 0.42])

FIGURE 13.5 Object detection with cross-correlation method. (a) Grayscale image with target highlighted as dotted rectangle and is also reproduced in the inset, (b) resulting grayscale images after correlation, (c) images after postprocessing.

scene. In this case, a particular treetop image is selected as the object, and is located in the whole image using the convolution method. The resulting image is then thresholded for the points of maximum correlation, which ultimately gives the tree count.

The same technique is applied to the sample images of Figure 13.2(a), and the results are shown in Figure 13.5. As can be seen in Figure 13.5, the exact location is slightly shifted from the center of the target image due to convolutional drifts.

# 13.6 COLOR-BASED TRACKING

Tracking objects based on color is one of the quickest and easiest methods for tracking an object from one image frame to the next. The speed of this technique makes it very attractive for near real-time applications, but due to its simplicity, many issues exist that can cause the tracking to fail.