# 12.3 Proposed System Functions

A GUI of palmprint recognition has been developed and its performance has been tested on the centralized databases. The functionalities of the palmprint GUI system are as follows.

# 12.3.1 Panel 1: Basic Operations

This panel contains *Load Image* and *Reset* buttons which are used to upload the input palmprint image from the database using *imread()* function and to restart the process of the system, respectively.

# 12.3.2 Panel 2: Histogram

Histogram and histogram equalization are techniques that modify the image by changing its intensity to the desired shape. Histogram technology maps the pixel intensity value of the input image to the output image using nonlinear and nonmonotonic transfer functions. The histogram of an image is the relative frequency of different grey levels. In a two-dimensional diagram, the x-axis shows grey levels, and the y-axis shows the number of pixels for each grey level. Using a monotonic, non-linear mapping, the histogram equalization reassigns the pixel intensity values in the input image so that the output image contains a uniform distribution of the intensities. Therefore, histogram equalization is generally used to enhance the contrast of an image [61]. Figure 12.3 shows the histogram and histogram-equalized image of a palmprint. The function *imhist()* is used to generate the histogram for the palmprint image and *histeq()* is used to equalize the histogram.

![](bbox=[0.148, 0.598, 0.853, 0.863])

**FIGURE 12.3**  
Histogram and histogram equalization of an image.