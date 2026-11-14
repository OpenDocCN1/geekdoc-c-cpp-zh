+   - Image analysis
+       - Image statistics
+       - Binary operations
+       - Region of interest operations
+   - Image understanding
+       - Image classification
+       - Image registration
+       - Image clustering
+       - Target identification and tracking

We will focus on the fundamental concepts of the main categories to the extent needed by most engineering curricula requirements. Occasionally, advanced topics as well as open areas of research will be pointed out. Further, we will restrict ourselves to two-dimensional (2D) image processing, although most of the concepts and techniques that are to be described can be extended easily to three or more dimensions.

# 1.1.1 What Is an Image?

A digital image is a 2D signal in essence, and is the digital version of the 2D manifestation of the real-world 3D scene. Although the words picture and image are quite synonymous, we will make the useful distinction that “picture” is the analog version of “image.” An image is a function of two real variables, for example, a(x,y) with a as the amplitude (e.g., brightness) of the image at the real coordinate position (x,y). An image may be considered to contain subimages, which are sometimes referred to as regions or regions of interest (ROIs). The amplitudes of a given image will almost always be either real numbers or integers. The latter is usually the result of a quantization process that converts a continuous range (say, between 0 and 100%) to a discrete number of levels.

# 1.2 DIGITAL IMAGE DEFINITIONS: THEORETICAL ACCOUNT

A digital image a[m,n] described in a 2D discrete space is derived from an analog image a(x,y) in a 2D continuous space through a sampling process that is frequently referred to as digitization. Each sample of the image is