various forms of the FFT, and most of them restrict the size of the input image that may be transformed, often to N = 2^n, where n is an integer. The mathematical details are well described in the literature.

The Fourier transform produces a complex number-valued output image that can be displayed with two images, either with the real and imaginary part or with the magnitude and phase. In image processing, often only the magnitude of the Fourier transform is displayed, as it contains most of the information of the geometric structure of the spatial domain image. However, if we want to retransform the Fourier image into the correct spatial domain after some processing in the frequency domain, we must make sure to preserve both magnitude and phase of the Fourier image.

The Fourier transform is used if we want to access the geometric characteristics of a spatial domain image. Because the image is in the Fourier domain is decomposed into its sinusoidal components, it is easy to examine or process certain frequencies of the image, thus influencing the geometric structure in the spatial domain.

In most implementations, the Fourier image is shifted in such a way that the DC value (i.e., the image mean), F(0,0), is displayed in the center of the image. The farther away from the center an image point is, the higher is its corresponding frequency. Figure 5.1 shows an example of application of the Fourier transform to images.

It can be seen that the R, G, and B layers are not providing more information than any single layer; therefore, it is always advisable for Fourier transform applications to work with grayscale images. Figure 5.2 shows the effect of changes in orientation of the original image.

# 5.3 WAVELET TRANSFORMS

Unlike the Fourier transform, in which the basis functions cover the entire signal range with frequency variation only, the wavelet transform performs better decomposition of a signal into its components because in this case, the basis functions vary in both frequency range (called scale) and spatial range. High-frequency basis covers a smaller area, whereas low-frequency basis covers a larger area. This transform is more appropriate for nonstationary signals and provides nonuniform partitions of frequency and spatial ranges.

In Fourier analysis, a signal is broken up into sine and cosine waves of different frequencies, and it effectively rewrites a signal in terms of different sine and cosine waves. Wavelet analysis does a similar thing: It takes a mother wavelet, and the signal is translated into shifted and scaled versions