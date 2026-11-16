# 2. Implement edge detectors

(a) Write a program to apply the following two kernels (referred to in the literature as the “Sobel operators”) to images SYNTH1.ifs, BLUR1.ifs, and BLUR1.V1.ifs.

| -1 | 0 | 1 |
| -2 | 0 | 2 |
| -1 | 0 | 1 |

| -1 | -2 | -1 |
| 0 | 0 | 0 |
| 1 | 2 | 1 |

To accomplish this, perform the following:

+   i. Apply \( h_x \) (see above) to the input, save the result as a temporary image in memory (remember that the numbers CAN be negative).
+   
+   ii. Apply \( h_y \) to the input, save the result as another array in memory.
+   
+   iii. Compute a third array in which each point in the array is the sum of the squares of the corresponding points in the two arrays you just saved. Finally, take the square root of each point. Save the result.
+   
+   iv. Examine the values you get. Presumably, high values are indicative of edges. Choose a threshold value and compute a new image, which is one whenever the edge strength exceeds your threshold and is zero otherwise.
+   
+   v. Apply steps 1–4 to the blurred and noisy images as well.

(b) Write a report. Include a printout of all three binary output images. Are any edge points lost? Are any points artificially created? Are any edges too thick? Discuss sensitivity of the result to noise, blur, and choice of threshold. Be thorough; this is a research course that requires creativity and exploring new ideas, as well as correctly doing the minimum required by the assignment.

**Assignment 5.5:** In Assignment 5.2, you derived a \( 5 \times 5 \) kernel that estimates \( \frac{\partial^2 f}{\partial x^2} \). Repeat Assignment 5.4 with the same images created, using that kernel for \( \frac{\partial^2 f}{\partial x^2} \) and the appropriate version for \( \frac{\partial^2 f}{\partial y^2} \).

**Assignment 5.6:** Verify the mathematics we did in Eq. 5.21. Those equations only show the x derivative for a one-dimensional Gaussian. To get the derivative to work correctly, it should differentiate in one direction and blur in the other. This requires the two-dimensional form of the Gaussian. Find a \( 3 \times 3 \) kernel that implements the derivative-of-Gaussian vertical edge operator of Eq. 5.21. Use \( \sigma = 1 \) and \( \sigma = 2 \) and determine two kernels. Repeat for a \( 5 \times 5 \) kernel. Discuss the impact of the choice of \( \sigma \) and its relation to kernel size. Assume the kernel may contain real (floating point) numbers. Suppose the kernel can only contain integers. Develop kernels that produce approximately the same result.

**Assignment 5.7:** In section 5.4.4, parameters useful for developing discrete Gaussian kernels were discussed. Prove that the value of \( \sigma \) such that the maximum of the second derivative occurs at \( x = -1 \) and \( x = 1 \) is \( \sigma = 1/\sqrt{3} \).

**Assignment 5.8:** Use the method of fitting a polynomial to estimate \( \frac{\partial^2 f}{\partial y^2} \). Which of the following polynomials would be most appropriate to choose?

+   (a) \( f = ax^2 + by + cxy \) (b) \( f = ax^3 + by^3 + cxy \)
+   
+   (c) \( f = ax^2 + by^2 + cxy + d \) (d) \( f = ax + by + c \)