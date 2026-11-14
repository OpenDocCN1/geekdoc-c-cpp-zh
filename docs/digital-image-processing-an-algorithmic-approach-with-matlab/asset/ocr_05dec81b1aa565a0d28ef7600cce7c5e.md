![](bbox=[0.1, 0.07, 0.92, 0.48])

FIGURE 4.6 Algorithmic structures of noise and blur addition to images.

represented either by the Poisson distribution or spotted randomness. The Poisson distribution is used in a limited number of algorithms, especially for thermal imaging and atmospheric imaging for remote sensing applications. However, in the remaining types, a spotted noise is added and is usually called salt-and-pepper noise. The name is appropriate because it only changes the intensity at random places to either a very bright (salt) or a very dark (pepper) pixel.

Blur, on the other hand, is more involved than noise. It requires a specific PSF represented as a smaller matrix as the manifestation of the blurring function. This small matrix is then convolved with the source image to produce the blurred version. The mechanics of convolution will be discussed in Chapter 6. Figure 4.6 represents the algorithms for introducing noise and blur in an image.

# 4.7 MATLAB CODE

In this section, the MATLAB code used to generate all the images in this chapter is presented.