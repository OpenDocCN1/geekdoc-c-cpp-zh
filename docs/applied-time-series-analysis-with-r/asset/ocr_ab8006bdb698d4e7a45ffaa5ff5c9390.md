# Wavelets

# 537

![](bbox=[0.143, 0.123, 0.849, 0.335])

FIGURE 12.23
(a) Barbara image (n = 256) and (b) DWT of Barbara image.

**Using R:** The two-dimensional plots in Figures 12.22a and 12.23a are based on the data sets xbox and barb in waveslim and plotted using the base R function image. The two-dimensional DWT's in Figures 12.22b and 12.23b were computed using the function dwt.2d and plotted using the function plot.dwt.2d (both functions are available in waveslim). See Appendix 12B for more details.

# 12.4 Concluding Remarks on Wavelets

This section on wavelets has a brief introduction of wavelet methods with a focus on time series applications. Wavelets have proven to be very useful in a variety of applications. We have discussed the use of wavelets for time–frequency analysis. We have discussed the fact that the wavelet transformation can provide a sparse representation of a data set, that is, to characterize a time series or image based on a small fraction of the number of values in the original data set. This capability proves to be very useful in applications. For example, these sparse representations lead to useful data compression methods such as the common JPEG image which is a compressed image format based on the discrete cosine transform. Strang and Nguyen (1997) for further discussion of data compression techniques and applications. Also consider the application of image analysis in which statistical decisions need to be made concerning the detection of certain features of an image. For example, in the analysis of a statistic map from an fMRI experiment, investigators wish to detect regions of brain activity. A typical two-dimensional brain slice from a functional magnetic resonance imaging