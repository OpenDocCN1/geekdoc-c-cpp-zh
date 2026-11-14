Image distortion: A situation in which the image is not exactly true to scale with the object scale.

Image enhancement: Image processing operations that improve the visibility of image detail and features. Usually performed either automatically by software or manually by a user through an interactive application. Any one or a group of operations that improves the detectability of the targets or categories. These operations include, but are not limited to, contrast improvement, edge enhancement, spatial filtering, noise suppression, image smoothing, and image sharpening.

Image filter: A mathematical operation performed on a digital image at every pixel value to transform the image in some desired way.

Image processing: Conversion of an image into another image in order to highlight or identify certain properties of the image.

Image resampling: A technique for geometric correction in digital image processing. Through a process of interpolation, the output pixel values are derived as functions of the input pixel values combined with the computed distortion. Nearest neighbor, bilinear interpolation, and cubic convolution are commonly used resampling techniques.

Kernel: A kernel is (usually) a small matrix of numbers that is used in image convolutions. Different-sized kernels containing different patterns of numbers give rise to different results under convolution. The word kernel is also commonly used as a synonym for structuring element, which is a similar object used in mathematical morphology.

Masking: A mask is a binary image consisting of both zero and nonzero values. If a mask is applied to another binary or to a grayscale image of the same size, all pixels that are zero in the mask are set to zero in the output image. All other pixels remain unchanged. Masking can be implemented using either pixel multiplication or logical AND, the latter in general being faster. Masking is often used to restrict a point or arithmetic operator to an area defined by the mask. We can, for example, accomplish this by first masking the desired area in the input image and processing it with the operator, then masking the original input image with the inverted mask to obtain the unprocessed area of the image and, finally, recombining the two partial images using image addition. In some image processing packages, a mask can directly be defined as an optional input to a