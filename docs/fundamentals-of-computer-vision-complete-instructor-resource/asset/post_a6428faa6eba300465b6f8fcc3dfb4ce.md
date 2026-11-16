
### Assignment 5.9

Fit the following expression to pixel data in a \( 3 \times 3 \) neighborhood: \( f(x, y) = ax^2 + bx + cy + d \). From this fit, determine a kernel that will estimate the second derivative with respect to \( x \).

### Assignment 5.10

Use the function \( f = ax^2 + by^2 + cxy \) to find a \( 3 \times 3 \) kernel that estimates \( \frac{\partial^2 f}{\partial x^2} \). Which of the following is the kernel that results? (Note: the following answers do not include the scale factor. Thus, the best choice below will be the one proportional to the correct answer.)

- (a)

| 6 | 4 | 0 |
| 4 | 6 | 0 |
| 0 | 0 | 4 |

- (b)

| 2 | 6 | 2 |
| -4 | 0 | -4 |
| 2 | 6 | -2 |

- (c)

| 6 | 4 | 0 |
| 4 | 6 | 0 |
| 0 | 0 | 1 |

- (d)

| 1 | -2 | 1 |
| 3 | 0 | 3 |
| 1 | -2 | 1 |

- (e)

| 1 | 0 | -1 |
| -2 | 0 | 2 |
| 1 | 0 | -1 |

- (f)

| 1 | 2 | 1 |
| -2 | 0 | -2 |
| -1 | -2 | -1 |

### Assignment 5.11

What does the following expression estimate? \( (f \otimes h_1)^2 + (f \otimes h_2)^2 = E \) where the kernel \( h_1 \) is defined by

| 0.05 | 0.08 | 0.05 |
| -0.136 | -0.225 | -0.136 |
| 0.05 | 0.08 | 0.05 |

and \( h_2 \) is created by the transpose. Choose the best answer

- a) The first derivative with respect to x (where x is the horizontal direction)
- b) The second derivative with respect to x
- c) The Laplacian
- d) The second derivative with respect to y
- e) The quadratic variation

### Assignment 5.12

You are to use the idea of differentiating a Gaussian to derive a kernel. What variance does a one-dimensional (zero mean) Gaussian need to have to have the property that the extrema of its first derivative occur at \( x = \pm 1 \)?

### Assignment 5.13

What is the advantage of the quadratic variation as compared to the Laplacian?

### Assignment 5.14

Let \( E = (f - Hg)^T(f - Hg) \). Using the equivalence between the kernel form of a linear operator and the matrix form, write an expression of \( E \) using kernel notation.

### Assignment 5.15

The purpose of this assignment is to walk you through the construction of an image pyramid, so that you will more fully understand the potential utility of this data structure, and can use it in a coding and transmission application. Along the way, you will pick up some additional understanding of the general area of image coding. Coding is not a principal learning objective of this course, but in your research career, you are sure to encounter people who deal with coding all the time. It will prove to be useful to have a grasp of some of the more basic concepts.

- 1. Locate the image specified by your instructor. Let's call that image XXX512. Verify that it is indeed 512 x 512. If it is not 512 x 512, then first write a program that will pad it out to that size.

- 2. Write a program that will take a two-dimensional n x n image and produce an image, of the same data type, which is n / 2 x n / 2. The program name should be ShrinkByTwo and called by

```
ShrinkByTwo inimg outimg
```

The program should not simply take every other pixel. Instead, each pixel of the output image should be constructed by averaging the corresponding four pixels in the input image. Note the requirement that the output image be of the same type as the input. Use your program to create XXX256, XXX128, XXX64, and XXX32. Don't bother with going below a 32 x 32 image. Turn in your program and a print of your images.

- 3. Write a subroutine to zoom an image. It should have the following calling convention:

```
ZoomByTwo(inimg, outimg)
```

The calling program is responsible for creating, reading, etc. of the images. The subroutine simply fills outimg with a zoomed version of inimg. Use any algorithm you wish to fill in the missing pixels. (We recommend that the missing pixels be some average of the input pixels.)

Before we can proceed, we need to consider a "pyramid coder". When you ran ShrinkByTwo, the set of images you produced is the pyramid representation of XXX512. In a pyramid coder, the objective is to use the pyramid representation to transmit as little information as possible over the channel. Here is the idea: First, transmit all of XXX32. Then, both the transmitter and receiver run ZoomByTwo to create a zoomed version of XXX32, something like

```
ZoomByTwo(XXX32,a64prime)
```

When we created XXX32 from XXX64, we threw away some information, and we cannot easily get it back, so a64prime will not be identical to XXX64. If, however, ZoomByTwo (which in the image coding literature, is called the "predictor") is pretty good, the difference between a64prime and XXX64 will be small (small in value that is, it is still 64 x 64). Therefore, compute diff64, the difference between a64prime and XXX64. If the predictor were perfect, the resultant difference would be a 64 x 64 image of all zeros, which could be coded in some clever way (by run-length encoding for example), and transmitted with very few bits. Let us now transmit diff64 to the receiver. By simply adding diff64 to the version of a64prime generated at the receiver, we can correct the errors made by the predictor, and we now have a correct version of XXX64 at the receiver, but all we transmitted was diff64. Clever, aren't we?

Now, from XXX64, we play the same game and get XXX128 created by transmitting diff128, etc cetera, ad nauseam. Now, the assignment:

- 4. Create the images described above, diff64, diff128, diff256, diff512. Measure the approximate number of bits required to transmit each of them. To make that measurement: Compute the standard deviation of, say, diff64. Take the log base 2 of that standard deviation, and that is the average number of bits per pixel required to code that image. Assume you were to transmit XXX512 directly. That would require 512 x 512 x 8 bits (assuming the image is 8 bits; you better verify!). Now, compare with the performance of your pyramid coder by adding up all the bits/pixel you found for each of the diff images you transmitted. Did your coder work well? Discuss this in your report.

### Assignment 5.16

At high levels of scale, only ______________ object are visible. (fill in the blank)

## Bibliography

- [5.1] M. Alfaraj, Y. Wang, and Y. Luo. Enhanced isotropic gradient operator. Geophysical Prospecting, 62, 2014.
- [5.2] V. Anh, J. Shi, and H. Tsai. Scaling theorems for zero crossings of bandlimited signals. IEEE Trans. Pattern Anal. and Machine Intel., 18(3), 1996.
- [5.3] J. Babuad, A. Witkin, M. Baudin, and R. Duda. Uniqueness of the Gaussian kernel for scale-space filtering. IEEE Trans. Pattern Anal. and Machine Intel., 8(1), 1986.
- [5.4] G. Biberbo and W. Snyder. Optimization of functions with many minima. IEEE Transactions on SMC, 21(4), July/August 1991.
- [5.5] P. Burt and E. Adelson. The Laplacian pyramid as a compact image code. CVGIP, 16, 1981.
- [5.6] J. Canny. A computational approach to edge detection. IEEE Trans. Pattern Anal. and Machine Intel., 8(6), 1986.
- [5.7] J. Crowley. A Representation for Visual Information, Ph.D. Thesis. CMU, 1981.
- [5.8] J. Daugman. Two-dimensional spectral analysis of cortical receptive fields. Vision Research, 20, 1980.
- [5.9] J. Daugman. Uncertainty relation for resolution in space, spatial frequency, and orientation optimized by two-dimensional visual cortical filters. J. Optical Soc. America, 2(7), 1985.
- [5.10] W. Frei and C. Chen. Fast boundary detection: A generalization and a new algorithm. IEEE Transactions on Computers, 25(2), 1977.
- [5.11] R. Haralick and L. Shapiro. Computer and Robot Vision, volume 1. Addison-Wesley, 1992.
- [5.12] M. Van Horn, W. Snyder, and D. Harrington. A radial filtering scheme applied to intracoronary ultrasound images. Computers in Cardiology, Sep. 1993.
- [5.13] D. Hubel and T. Wiesel. Receptive fields, binocular interaction, and functional architecture in the cat's visual cortex. Journal of Physiology (London), 160, 1962.
- [5.14] D. Hubel and T. Wiesel. Functional architecture of macaque monkey visual cortex. Proceedings of the Royal Society, B, 198, 1978.
- [5.15] P. Jackway and M. Deriche. Scale-space properties of the multiscale morphological dilation-erosion. IEEE Trans. Pattern Anal. and Machine Intel., 18(1), 1996.
- [5.16] J. Jones and L. Palmer. An evaluation of the two-dimensional gabor filter model of simple receptive fields in the cat striate cortex. J. Neurophysiology, 58, 1987.
