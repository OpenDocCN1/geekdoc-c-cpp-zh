and columns of the image. Higher resolution means more image detail. Consequently, image resolution can be tied to physical size (e.g., lines per millimeter, lines per inch) or to the overall size of a picture (lines per picture height, number of pixels, and pixel density).

# 1.3 IMAGE PROPERTIES

# 1.3.1 Signal-to-Noise Ratio

Signal-to-noise ratio (SNR) is an important parameter to judge, analyze, and classify several image processing techniques. As described previously, in modern camera systems the noise is frequently limited by the following:

+   - Amplifier noise in the case of color cameras
+   - Thermal noise, which itself is limited by the chip temperature K and the exposure time T
+   - Photon noise, which is limited by the photon production rate and the exposure time T

Effectively, SNR is calculated as

```
SNR = \frac{Signal\_Power}{Noise\_Power} = 20log \frac{P_{Signal}}{P_{Noise}} (1.1)
```

How noise can affect the image is shown in Figure 1.2. The added noise is of “salt-and-pepper” type. The addition of noise is only the addition of randomness to the clean pixel values. This, however, is a very common problem in digital image acquisition, where the randomness appears from hardware elements. Chip behavior can be random on account of thermal conditions; such behavior is inherently a charge flow phenomenon and is highly dependent on the temperature.

# 1.3.2 Image Bit Resolution

Image bit resolution, or simply image resolution, refers to the number of grayscale levels or the number of pixels present in the image. Compared to the term spatial resolution mentioned earlier (following Figure 1.1), the commonly used terminology of image resolution refers to the representational capability of the image, using a certain number of bits to represent