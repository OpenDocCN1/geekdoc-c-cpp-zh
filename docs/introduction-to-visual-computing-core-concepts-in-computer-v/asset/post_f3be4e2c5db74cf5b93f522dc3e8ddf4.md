
He was ordained in the Roman Catholic Church and sent to the University of Caen to read theology at the age of 16. At the university, two enthusiastic teachers of mathematics, Christophe Gadbled and Pierre Le Canu, inspired his zeal for the subject. His brilliance as a mathematician was quickly recognized and while still at Caen he wrote his first paper in a journal founded by Lagrange. Recognizing that he did not have any inclination towards priesthood, Laplace became an atheist, broke away from the church and left for Paris to become the student of Jean le Rond d’Alembert (famous today for Lambertian reflectance models). Lambert tried to get rid of Laplace initially by giving him impossible assignments of reading tough math books and solving unsolved math problems. But when Laplace’s brilliance allowed him to complete such tasks in much less time than was provided, he took him under his wings and recommended a teaching position in the Royal Military Academy of Belgium where Laplace devoted his time to path breaking research for the next seventeen years. Laplace became a count of the First French Empire in 1806 and was named a marquis (nobleman) in 1817. He died in 1827. Intrigued by the magnitude of his brilliance, his physician removed his brain and preserved it before it was displayed in an anatomical museum in Britain. It was reportedly much smaller than the average human brain.

To arrive at this intuitive result, we will still do the convolution, but first we will subtract the mean of all the pixel colors from the template and the region of the image it is overlapping with before performing the convolution. This is shown in the right image of Fig 3.20 where the mean is also indicated by μ. Note that now the convolution provides us with what we expected from the correlation operation intuitively. The blue window has the highest value of 1, the red window has the lowest value of −1 and the yellow and green windows have a value of 0 which is halfway between −1 and 1. Also, note that the value at the purple window is negative making it closer to the red window than the blue window. Therefore, convolution when used on functions offset by their mean, can be used to find the extent of similarity between a template and a region in the image. This process is called *cross-correlation*.

Recall that convolution usually involves flipping the impulse response which we did not need to do in this chapter (and in many image processing applications) since we deal with symmetric filters most of the time. The way cross-correlation differs from convolution is that the flipping of the kernel is not required.

Next, let us take another perspective to this cross correlation. You can think of it as an element wise multiplication of the template elements with the underlying image elements with which the template overlaps and then adding them up. Does this remind you of anything? Well, this is a dot product of two vectors, one vector consisting of the elements of the template and the other made up of the elements of the region of the image with which the template overlaps. The value of the dot product gives an estimate of how close is one vector to another. The dot product of 1 signifies identical vectors, the dot product of zero signifies orthogonal vectors and the dot product of −1 signifies opposite vectors. Notice that the same thing holds for cross correlation.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_76_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_76_1.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_76_2.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_76_3.png)

Figure 3.21. On the left is an image and the template to be matched in the image. In the middle is the result of the process of normalized cross correlation. On the right is the template (in color) superimposed at the location given by the highest value of the normalized cross-correlation finding an exact match.

Now, you probably remember that while performing dot products for vectors, they needed to be normalized. This was to make sure that we are only considering the directions of the vectors and not their magnitudes. The values of this dot product range between −1 to +1 only when such normalization is applied. Our subtraction of the mean, as shown in Figure 3.21, was an attempt to approximate this normalization. But a subtraction does not affect the magnitude of the colors to assure unit vectors. Therefore, ideally, we should subtract the mean and divide with the standard deviation, given by the square root of the sum of squared differences of each value from the mean. This step would achieve the desired normalization.

What does this normalization mean in the context of image processing. Fundamentally, cross-correlation is a way to examine if any part of the image matches with a template image. Ideally, we should be able to do this matching irrespective of three factors changing between the two images: (a) scene illumination; (b) the camera exposure that decides the brightness of the image; and (c) the camera gain that decides the contrast of the image. The normalization allows us to make the cross-correlation robust against these three changes and is often called normalized cross-correlation.

## 3.3 Implementation Details

This brings us to the end of the fundamental concepts behind the linear system and convolution. However, you may still find some challenges when implementing convolution. So, following are the things to be remembered for this purpose.

- 1. When performing convolution of a filter with an image, it is important to align the filter with every pixel and then apply the convolution. Note that the result of convolution at each pixel should be stored in a different image. Otherwise it will affect the convolutions at other pixels performed later.
- 2. If the filter size is an even number, you will not be able to find a central pixel to align with the image pixel at which convolution is being performed. The common thing to do in this case is to align the image pixel with the top left pixel of the filter. This will shift the image by half the size of the kernel in each direction and should be shifted back after the operation.
- 3. When the filter overlaps an area outside the edge of the image, the pixel values of those pixels are undefined. What should we do then? Usually you can pad the image with 0 or 1 or by reflecting the image about the edge or any other way you choose. What is chosen does not matter since these will only contribute to the samples that are not fully immersed and hence should be ignored from a data accuracy perspective.
- 4. Convolution is made of many floating point operations while images are usually stored as 8-bit integers. Performing floating point operations on integers results in accumulation of errors at every step of the operation (e.g. every multiplication and addition). The best way to handle this is to first convert the image and the filter into a floating point representation, perform the filtering and then round it back to the integer representation.
- 5. Finally, sometimes convolution can lead to out-of-range values in the resulting image (beyond 0 to 1 or beyond 0 to 256). The best way to handle this is to find the minimum and maximum values after the operation and scale the image back to be within range.

## 3.4 Conclusion

In this chapter you were introduced to one of the most fundamental concepts of visual computing — systems and their responses and how to find responses of arbitrary inputs to the systems. We have tried to give you a less mathematical and more engineering view of convolution which is directly applicable to digital image processing. To get a more mathematical treatise of the subject, especially considering general multi-dimensional continuous signals, please refer to [Pratt 07, Gonzalez and Woods 06].

## Bibliography

- [Gonzalez and Woods 06] Rafael C. Gonzalez and Richard E. Woods. *Digital Image Processing (3rd Edition)*. Prentice-Hall, Inc., 2006.
- [Pratt 07] William K. Pratt. *Digital Image Processing*. John Wiley and Sons, 2007.
