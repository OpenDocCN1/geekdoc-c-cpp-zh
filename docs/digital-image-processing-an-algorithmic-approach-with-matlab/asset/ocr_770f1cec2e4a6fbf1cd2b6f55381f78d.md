pixel separately using a mask. The size of the mask must be identical with the size of the images.

# 3.4 ALGORITHMIC TREATMENT

In this section, details related to algorithmic structures and usage of the operators mentioned in Section 3.3 will be presented. The emphasis is on presenting the algorithms in a generic manner so that they can be programmed in any language.

# 3.4.1 Image Addition

Figure 3.2(a) represents the algorithmic structure for adding two images. Obviously, the operation is repetitive and can be realized using any recursive programming approach, including loops, or a recursive function call. Image addition is usually a supportive operation rather than an operation on its own in image processing. For example, a constant value can be added to the image to brighten up the view, or enhanced edges can be added in an image to sharpen the object linings and new images can be generated through addition of two or more other images.

One important point to be mentioned here is the fact that although the theory presented or the equations mentioned all deal with two images or an image with a scalar, the same approach can be extended to more than two images by repeating the algorithms as need.

# 3.4.2 Image Subtraction/Multiplication/Division

Once the operation for addition is understood from Section 3.4.1, the remaining three operations, subtraction, multiplication, and division, can be considered similarly. As can be seen from Figures 3.2(b), (c), and (d), the algorithms are exactly the same as for addition except for the main processing operation, which is changed according to the desired operations. Hence, the calculation requirements change at the pixel level only, which also depends on the processor in use and the way in which these operators are implemented at the hardware level.

Image subtraction can be used as a preliminary step in more complex image processing, or by itself. For example, one can use image subtraction to detect changes in a series of images of the same scene, or subtraction can be used to separate the foreground artifacts from background for applications such as target detection, scene analysis, localized processing, and