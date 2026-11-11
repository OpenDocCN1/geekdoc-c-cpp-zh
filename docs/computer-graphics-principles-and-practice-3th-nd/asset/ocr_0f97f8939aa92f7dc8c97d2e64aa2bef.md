# # Chapter 19

# # Enlarging and Shrinking Images

# ## 19.1 Introduction

In Chapters 17 and 18 you learned how images are used to store regular arrays of data, typically representing samples of some continuous function like "the light energy falling on this region of a synthetic camera's image plane." You also learned a lot of theoretical information about how you can understand such sampled representations of functions by examining their Fourier transforms. In this chapter, we apply this knowledge to the problems of adjusting image sizes (scaling images up and down, as shown in Figure 19.1, which are synonyms for "enlarging" and "shrinking"), and performing various operations such as edge detection.

We assume that the values stored in an image array form a signal that is real-valued, *not* discrete; nothing we say here applies to an object-ID image, for example.

Just as we did in Chapter 18, in this chapter we study primarily grayscale images. Scaling up or down a grayscale image entails all the main ideas without the complications of three color channels. Furthermore, we continue to study the effects of transformations on a single row of image pixels, because the extension to two dimensions really has no important properties beyond those of one dimension, but the notation is substantially more complex. We do, however, return to two dimensions when providing code for scaling up and down, and when we analyze the efficiency of computing convolutions.

In this chapter, we use the following ideas from Chapter 18.

+   - Sampling and convolution operations on a signal can be profitably viewed in both the value and the frequency domains.
+   - The convolution-multiplication theorem. Convolution in the value domain corresponds to multiplication in the frequency domain, and vice versa.

![](bbox=[0.707, 0.48, 0.933, 0.64])

*Figure 19.1: Terminology for image scaling.*