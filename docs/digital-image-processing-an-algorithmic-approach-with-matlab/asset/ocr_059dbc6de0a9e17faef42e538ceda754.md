\(\xi(q) = \begin{cases} \frac{1}{\sqrt{2}} & \text{for } q=0 \\ 1 & \text{otherwise} \end{cases} \quad (8.5)\)

The main advantages of the DCT are that it yields a real-valued output image and that it is a fast transform. After performing a DCT, it is possible to throw away the coefficients that encode those frequency components that the human eye is not very sensitive to. Thus, the amount of data can be reduced, without seriously affecting the way an image looks to the human eye. The inverse transform for Equation 8.3 is given by

\(f(m,n) = \frac{1}{4} \sum_{p=0}^{N-1} \sum_{q=0}^{N-1} \psi(p)\xi(q) F(p,q) \cos\left(\frac{(2m+1)p\pi}{2N}\right) \cos\left(\frac{(2n+1)q\pi}{2N}\right). \quad (8.6)\)

The definition of the coefficient multipliers remains the same as in Equations 8.4 and 8.5. Figure 8.1 shows the application of DCT and inverse DCT to the cameraman image.

# 8.4 BIT ALLOCATION

The first step in compressing an image is to segregate the image data into different classes. Depending on the importance of the data it contains, each class is allocated a portion of the total bit budget such that the compressed image has the minimum possible distortion. This procedure is called bit allocation.

The rate-distortion theory is often used for solving the problem of allocating bits to a set of classes, or for bit-rate control in general. The theory aims at reducing the distortion for a given target bit rate by optimally allocating bits to the various classes of data. One approach to solving the problem of optimal bit allocation is through using the rate-distortion theory explained as follows:

+   1. Initially, all classes are allocated a predefined maximum number of bits.
+   
+   2. For each class, one bit is reduced from its quota of allocated bits, and the distortion due to the reduction of that one bit is calculated.