
where h(m,n) represents the degradation model, and ⊗ represents the 2D convolution operation. The additive term η(m,n) represents the noise added to the degraded image, further increasing the distortion of image. The blurring function in the main block is a function of the pixel coordinates m and n, and a parameter list θ. This list depends on the type of representation used for the blurring function. For instance, for a Gaussian function, the parameter list only comprises two parameters, mean and variance, and so on. In some applications, noise can also be considered multiplicative, in which case the restoration problem is more difficult than in the additive noise case. The function h(m,n) is also called the point spread function (PSF) in the image processing literature, and depends on the type of distortion or degradation.

The degradation h(m,n) can be convolved with the clean image because of several factors. Among them, the most prominent are hardware misalignment, malfunction, human errors, and electronic noise. In nearly any practical situation, a device of finite spatial extent records an image. As a result, not all the data that is needed to model the real object is available.

Convolution in the Fourier domain is identical in result to that in the spatial domain, in which a kernel of values (a blur function) is applied to every pixel in the image. In Fourier space, this simply involves multiplying the transform of the blur function with the transform of the image, pixel by pixel. In many cases, it will be easier to construct the kernel as an image rather than as a set of numerical values. This is particularly true when the kernel is not symmetrical. Sometimes, the blur function can be measured directly by acquiring an image of a point (e.g., a star in astronomical images). Some examples of such convolutions are shown applied to the car image in Figure 7.2.

This also implies that it is possible to remove blur from a blurred image by dividing by the transform of the blur, and this process is called deconvolution. It deconvolves the main image using the content of the image previously designated. Deconvolution is typically used to remove blur from an image due to out-of-focus optics or motion while capturing the image with a camera. There are other applications in which deconvolution can be employed, to remove specific blurring function. In general, when deconvolving such blurs, one image is the blurred image and a second image is used that contains information related to the PSF of the blur only. By using this second image in the same format as that of the blurred image, it facilitates the algorithmic procedures in terms of speed and memory requirements.

Figure 7.2 shows what it means to perform deconvolution. The car2.jpg image has first been convolved with two different types of blur or PSFs and

![](img/fc093ca9cc8a631842aa559a749dca54_149_0.png)

(a)

![](img/fc093ca9cc8a631842aa559a749dca54_149_1.png)

(b)

![](img/fc093ca9cc8a631842aa559a749dca54_149_2.png)

(c)

![](img/fc093ca9cc8a631842aa559a749dca54_149_3.png)

(d)

FIGURE 7.2 Example of deconvolution for two commonly occurring blurring problems. (a) Motion-blurred image, (b) deconvolved image, (c) out-of-focus blurred image, (d) deconvolved image.

then recovered correspondingly through the inverse process of deconvolution. The first example is a symmetrical blur as might be produced by out-of-focus optics, and the second is motion blur, which corresponds to a straight line (whose direction and distance must be known).

When the PSF can be measured from the image itself, for example, as the blurred image of a single star, a single fluorescent bead, or a single dust particle, it can be conveniently used for deconvolution. In other cases, it may be possible to estimate it from independent knowledge.

Frequency filters are also commonly used in image reconstruction. Here, the aim is to remove the effects of a nonideal imaging system by multiplying the image in the Fourier space with an appropriate function. The easiest method, called inverse filtering, is to divide the image in the Fourier space by the optical transfer function (OTF). We illustrate this deconvolution, using Figures 7.3 and 7.4.

## 7.3 DECONVOLUTION

Deconvolution is the reverse (at least theoretically) of convolution. When the degradation due to blur is to be removed, the process is not as simple as filtering out the noise. Because the blurring of the image is essentially a convolution of the clean image with the PSF of the blur, the principal procedure in any restoration scheme is finding out an inverse procedure to cancel out the effect of the blur PSF. This is also called deconvolution, or inverse filtering. Given the image model of Equation 7.1 without noise, then

$g = h \otimes f \Leftrightarrow G = HF, \quad (7.2)$

where, G, H, and F are the Fourier transforms for g, h, and f, respectively. Therefore, by inverse filtering or a deconvolution operation, the original image can be retrieved as follows:

$F = D^{-1}G \Leftrightarrow f = (\mathfrak{F}^{-1}h^{-1}) \otimes g, \quad (7.3)$

where $\mathfrak{F}^{-1}$ represents the inverse Fourier transform. This seemingly simple problem is not so simple in reality. In many practical cases, it is useless or even impossible to apply it as given by Equations 7.2 and 7.3. This is because the PSF is usually unknown and often zero over wide ranges. Hence, $h^{-1}$ will be infinite in this case.

If additive noise is considered for the inverse filtering problem, then the end result will be similar to Equation 7.3 but with an additional term, $h^{-1}\eta$. This means that even if H is nonzero, the noise will be amplified by a constant factor of $h^{-1}$. In effect, the signal-to-noise ratio in this case is not improved but stays the same because noise and the degraded system are amplified by the same factor.

There are three situations with respect to the blurring function and its know-how:

- White box problem: When h is precisely known
- Gray box problem: When partial information is available about h
- Black box problem: When nothing is known about the blurring function

When the blurring function h(m,n) is not accurately known, it must be estimated prior to inverse filtering. Because the attempt is to deconvolve the degraded image g(m,n) without any prior knowledge of the cause that is producing the degradation, such a procedure is also called blind deconvolution, as it is blind to the source of the degradation.

In MATLAB®, three main types of deconvolution algorithms have been implemented. This is by no means an exhaustive list, and newer methods keep popping up in the literature from time to time. The chief methods are

- 1. Lucy-Richardson Method
- 2. Wiener method
- 3. Blind method

The algorithms related to these methods are presented in Section 7.4. Figure 7.3 shows the results of using the Lucy-Richardson, Wiener, and blind deconvolution methods on the car2.jpg image. Specifically, for blind deconvolution, two initial blurring functions were tested. The first is a random matrix of size 5 x 5, and the second is the same blurring function that caused the blurring in the first place.

The same example is repeated in Figure 7.4 for the motion blur case, with motion affecting a neighborhood of 15 pixels and at 45°.

In general, these algorithms either use a known (or somewhat known) blurring function or try to estimate one iteratively. Usually, they rely on second-order statistics or H2 norms for their convergence. Optimal H2 filters (or Kalman filters) are suitable solutions to the filtering and estimation problem when the power spectral density of the noise is precisely known.

In general least-squares estimation problems, one minimizes the integral of the power spectral density estimation error. This minimization of the average error power or error variance might result in a relatively large error power in some frequency range. In many practical situations, however,
