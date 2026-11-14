
every pixel. The addition of two images is performed straightforwardly in a single pass. The output pixel values are given by

R(m,n) = P(m,n) + Q(m,n). (3.1)

where P, Q, and R represent the image matrices of the same size, and m and n represent the mth and nth pixels.

Alternatively, if it is simply desired to add a constant value C to a single image, then:

R(m,n) = P(m,n) + C. (3.2)

If each pixel value corresponds to an n-tuple instead of a number (for instance, the color image would have each pixel as a vector of three values corresponding to red, blue, and green components), then such pixels are operated on by addition at each corresponding vector element to produce the output value.

The results of addition can easily grow beyond the maximum value that the pixel bit resolution will allow. For 8-bit representation of pixels, the addition of two pixels with values of 200 each would result in 400, which is higher than the maximum representable number with 8 bits, 255. The overflowing pixel values are usually set to the maximum allowed value, an effect known as saturation.

### 3.3.2 Pixel Subtraction

The pixel subtraction operator takes two images as input and produces as output a third image whose pixel values are simply those of the first image minus the corresponding pixel values from the second image. It is also often possible to just use a single image as input and subtract a constant value from all the pixels. Some versions of the operator will output the absolute difference between pixel values rather than the signed output. The subtraction of two images is performed straightforwardly in a single pass. The output pixel values are given by

R(m,n) = P(m,n) - Q(m,n). (3.3)

Or if the operator computes absolute differences between the two input images, then:

R(m,n) = |P(m,n) - Q(m,n)|. (3.4)

Or if it is simply desired to subtract a constant value C from a single image, then:

R(m,n) = P(m,n) - C. (3.5)

If each pixel value corresponds to an n-tuple instead of a number (for instance, the color image would have each pixel as a vector of three values corresponding to red, blue, and green components), then such pixels are operated on by subtraction at each corresponding vector element to produce the output value.

If the operator calculates absolute differences and the two input images use the same pixel value type, then it is impossible for the output pixel values to be outside the range that may be represented by the input pixel type, and so this problem does not arise. This is one good reason to use absolute differences.

### 3.3.3 Pixel Multiplication and Scaling

Although images are treated as matrices, image multiplication does not follow the matrix multiplication rule. This implies that instead of having the number of columns of the first matrix be the same as the number of rows the second matrix, image multiplication requires the two images to be of the same size. Similar to other image arithmetic operators, multiplication comes in two forms. The first form takes two input images and produces an output image in which the pixel values are just those of the first image, multiplied by the values of the corresponding values in the second image. The second form takes a single input image and produces output in which each pixel value is multiplied by a specified constant. This latter form is probably more widely used and is generally called scaling. The multiplication of two images is performed in the obvious way in a single pass using the formula:

R(m,n) = P(m,n) × Q(m,n). (3.6)

Scaling by a constant is performed using

R(m,n) = P(m,n) × C. (3.7)

Note that the constant is often a floating-point number, and may be less than one, which will reduce the image intensities. It may even be negative if the image format supports that.

If each pixel value corresponds to an n-tuple instead of a number (for instance, the color image would have each pixel as a vector of three values corresponding to red, blue, and green components), such pixels are operated on by multiplication at each corresponding vector element to produce the output value. If the output values are calculated to be larger than the maximum allowed pixel value, then they are usually truncated at that maximum value. The same is also true for values less than the minimum allowed pixel values, in which case the truncation is done at the minimum value.

### 3.3.4 Pixel Division

The image division operator normally takes two images as input and produces a third image whose pixel values are the pixel values of the first image divided by the corresponding pixel values of the second image. Many implementations can also be used with just a single input image, in which case every pixel value in that image is divided by a specified constant.

The division of two images is performed in the obvious way, in a single pass using the formula:

R(m,n) = P(m,n) / Q(m,n). (3.8)

Division by a constant is performed using

R(m,n) = P(m,n) / C. (3.9)

If each pixel value corresponds to an n-tuple instead of a number (for instance, the color image would have each pixel as a vector of three values corresponding to red, blue, and green components), such pixels are operated on by division at each corresponding vector element to produce the output value.

The division operator may only implement integer division, or it may also be able to handle floating-point division. If only integer division is performed, then results are typically rounded down to the next lowest integer for output. The ability to use images with pixel value types other than 8-bit integers comes in very handy when doing division.

### 3.3.5 Blending

This operator produces a blend of two input images of the same size by combining scalar multiplication and image addition. Similar to pixel addition, the value of each pixel in the output image is a linear combination of the corresponding pixel values in the input images. The coefficients of the linear combination are user specified, and they define the ratio by which the images must be scaled before combining them. These proportions are applied such that the output pixel values do not exceed the maximum pixel value. The resulting image is calculated using the following formula:

R(m,n) = C × P(m,n) + (1-C) × Q(m,n). (3.10)

P and Q are the two input images. C is the blending ratio, which determines the influence of each input image in the output. C can either be a constant factor for all pixels in the image or can be determined for each pixel separately using a mask. The size of the mask must be identical with the size of the images.

## 3.4 ALGORITHMIC TREATMENT

In this section, details related to algorithmic structures and usage of the operators mentioned in Section 3.3 will be presented. The emphasis is on presenting the algorithms in a generic manner so that they can be programmed in any language.

### 3.4.1 Image Addition

Figure 3.2(a) represents the algorithmic structure for adding two images. Obviously, the operation is repetitive and can be realized using any recursive programming approach, including loops, or a recursive function call. Image addition is usually a supportive operation rather than an operation on its own in image processing. For example, a constant value can be added to the image to brighten up the view, or enhanced edges can be added in an image to sharpen the object linings and new images can be generated through addition of two or more other images.

One important point to be mentioned here is the fact that although the theory presented or the equations mentioned all deal with two images or an image with a scalar, the same approach can be extended to more than two images by repeating the algorithms as need.

### 3.4.2 Image Subtraction/Multiplication/Division

Once the operation for addition is understood from Section 3.4.1, the remaining three operations, subtraction, multiplication, and division, can be considered similarly. As can be seen from Figures 3.2(b), (c), and (d), the algorithms are exactly the same as for addition except for the main processing operation, which is changed according to the desired operations. Hence, the calculation requirements change at the pixel level only, which also depends on the processor in use and the way in which these operators are implemented at the hardware level.

Image subtraction can be used as a preliminary step in more complex image processing, or by itself. For example, one can use image subtraction to detect changes in a series of images of the same scene, or subtraction can be used to separate the foreground artifacts from background for applications such as target detection, scene analysis, localized processing, and
