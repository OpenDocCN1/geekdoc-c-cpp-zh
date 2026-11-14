![](bbox=[0.06, 0.06, 0.91, 0.5])

FIGURE 6.4 Effects of Gaussian filtering. (a) Noisy image with Gaussian noise; (b) filtered image for (a); (c) noisy image with salt-and-pepper noise; (d) filtered image for (c).

from this neighborhood are found, and the center pixel value is compared against these limiting values. If the value of the center pixel is above the maximum, it is set to the maximum value; if it is less than the minimum, it is set to the minimum value, else it is left as it is. Due to this selective replacement strategy, the chances of removing the outlier values, and consequently the speckle and salt-and-pepper noise, can be eliminated. Figure 6.5 shows this design strategy.

Figure 6.6 shows an example of the application of this filter. The effects can be fine-tuned by choosing a bigger neighborhood and experimenting with various signal-to-noise ratios as well as with different types of noise.

# 6.3 FREQUENCY-BASED FILTER DESIGN

Frequency filters process an image in the frequency domain. The image is Fourier-transformed, multiplied by the filter function, and then retrans-formed into the spatial domain. Attenuating high frequencies results in a