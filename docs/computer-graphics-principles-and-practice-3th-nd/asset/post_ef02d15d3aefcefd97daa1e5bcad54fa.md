
![](img/f464cd0043eb5336aa0543fe20a0561b_814_0.png)

*Figure 28.17:* The color-matching functions \(\bar{x}\), \(\bar{y}\), and \(\bar{z}\) for the 1931 CIE primaries.

- Because the red, green, and blue primaries can be identified as points in *XYZ*-space (i.e., as a linear combination of **X**, **Y**, and **Z**), any combination of them can be so expressed as well; thus, there's a direct conversion from *XYZ* to *RGB* coefficients (and vice versa).

In analogy with the color-matching functions for red, green, and blue, a light whose spectral power distribution is \(P\) can be expressed as

$$X\mathbf{X} + Y\mathbf{Y} + Z\mathbf{Z}, \qquad (28.17)$$

where

$$X = k \int P(\lambda)\bar{x}(\lambda)\,d\lambda, \qquad (28.18)$$

$$Y = k \int P(\lambda)\bar{y}(\lambda)\,d\lambda, \quad \text{and} \qquad (28.19)$$

$$Z = k \int P(\lambda)\bar{z}(\lambda)\,d\lambda. \qquad (28.20)$$

(More precisely: The light with power distribution \(X\mathbf{X} + Y\mathbf{Y} + Z\mathbf{Z}\) and the light with power distribution \(P\) will evoke the same color response.)

In practice, such integrations are computed numerically, using the values of the matching functions tabulated at 1 nm intervals that are found in texts such as [WS82, BS81]. The constant \(k\) is 680 lm W\(^{-1}\). But we also sometimes compute the “colors” for the reflectance spectrum of some reflecting object. In this case, one must choose a standard light source as a reference for “white” and illuminate the surface. The values are usually scaled so that a completely reflective surface has a \(Y\)-value of 100; thus,

$$k = \frac{100}{\int W(\lambda)\bar{y}(\lambda)\,d\lambda}. \qquad (28.21)$$

where \(W\) is the spectral power distribution of the standard white light we're using.

Suppose that the light \(C\) produces the same sensor responses as

$$XX + YY + ZZ. \qquad (28.22)$$

In that case, we write

$$C = XX + YY + ZZ. \qquad (28.23)$$

The CIE defines numbers that are independent of the overall brightness by dividing through by \(X + Y + Z\); doubling the incoming light doubles each of \(X\), \(Y\), and \(Z\), but also doubles their sum, so the quotients

$$x = \frac{X}{X + Y + Z}, \qquad (28.24)$$

$$y = \frac{Y}{X + Y + Z}, \quad \text{and} \qquad (28.25)$$

$$z = \frac{Z}{X + Y + Z}. \qquad (28.26)$$

remain unchanged. Note that the sum \(x + y + z\) is always 1, so if we know \(x\) and \(y\), we can compute \(z\). Thus, the collection of intensity-independent colors can be plotted on just the \(xy\)-plane; the result is the **CIE chromaticity diagram** shown in Figure 28.18. Note that **X** and **Y** were chosen so that the diagram is tangent to the \(x\)- and \(y\)-axes.

Near the center of the "horseshoe" is **illuminant C**, which is a standard reference "white," based on daylight. Unfortunately, it doesn't correspond to

![](img/f464cd0043eb5336aa0543fe20a0561b_815_0.png)

*Figure 28.18: The CIE chromaticity diagram. The boundary consists of chromaticities corresponding to monochromatic lights of the given wavelengths, shown in nanometers. The dot in the center is a standard "white" light called "illuminant C."*

## 28.9 Perceptual Color Spaces

The CIE color system is remarkably useful; it’s so standard that colorimeters measure \(X\), \(Y\), and \(Z\) values of light, for instance. In the CIE system, each color has \(XYZ\)-coordinates; it’s tempting to measure the “distance” between two colors \(C_1 = X_1\mathbf{X} + Y_1\mathbf{Y} + Z_1\mathbf{Z}\) and \(C_2 = X_2\mathbf{X} + Y_2\mathbf{Y} + Z_2\mathbf{Z}\) by computing the Euclidean distance between the triples \((X_1,Y_1,Z_1)\) and \((X_2,Y_2,Z_2)\). Unfortunately, this does not correspond to the perceived color distance: If \(C_1\) and \(C_2\) have the same Euclidean distance as \(C_3\) and \(C_4\), the perceived distance between them may be very different.

Fortunately, one can transform the \(XYZ\)-coordinates, nonlinearly, to get new coordinates in which the Euclidean distance does correspond to perceptual distance. The 1960 CIE \(Luv\) color coordinates were developed to meet this need, but they were superseded by the 1976 CIE \(L^*u^*v^*\) uniform color space. Letting \(X_w\), \(Y_w\), and \(Z_w\) denote the \(XYZ\)-coordinates of the color to be used as white, the \(L^*u^*v^*\)-coordinates of a color with \(XYZ\)-coordinates \((X,Y,Z)\) are defined by the formula for \(L^*\) given in Equation 28.10, and

$$u' = \frac{4X}{X+15Y+3Z}, \qquad (28.30)$$

$$v' = \frac{9Y}{X+15Y+3Z}, \qquad (28.31)$$

$$u'_w = \frac{4X_w}{X_w+15Y_w+3Z_w}, \qquad (28.32)$$

$$v'_w = \frac{9Y_w}{X_w+15Y_w+3Z_w}, \qquad (28.33)$$

$$u^* = 13L^*(u'-u'_w), \quad \text{and} \qquad (28.34)$$

$$v^* = 13L^*(v'-v'_w). \qquad (28.35)$$

The CIE has also defined \(L^*a^*b^*\) color coordinates (sometimes called “Lab” color) by

$$a^* = 500\left[\left(X/X_w\right)^{1/3} - \left(Y/Y_w\right)^{1/3}\right], \quad \text{and} \qquad (28.36)$$

$$b^* = 500\left[\left(Y/Y_w\right)^{1/3} - \left(Z/Z_w\right)^{1/3}\right]. \qquad (28.37)$$

where \(X_w\), \(Y_w\), and \(Z_w\) denote the \(XYZ\)-coordinates of the white point. Both \(L^*u^*v^*\) and \(L^*a^*b^*\) can be used to measure “distance” in color space, and both see frequent use in computer graphics, although \(L^*a^*b^*\) seems to be more widely used in the description of displayed colors.

### 28.9.1 Variations and Miscellany

The CIE diagram we’ve shown is based on the 1931 tabulation of colors, in which samples subtended a \(2^\circ\) field of view on the retina. There’s also a 1964 tabulation for a \(10^\circ\) field of view, explaining larger areas of constant color. For much of computer graphics, the narrower field of view is more relevant.

The mapping from the space of all spectra (which is infinite-dimensional) to the space of response triples (which is three-dimensional) is more or less linear

![](img/f464cd0043eb5336aa0543fe20a0561b_818_0.png)

*Figure 28.21: Two metameric light spectra (top) are each multiplied (wavelength by wavelength) by the reflectance spectrum (middle). The resultant spectra are no longer metameric. (Next to the spectrum for each light is its corresponding RGB response values.)*

(at least for not-too-bright lights, where saturation comes into play, and not-too-dim lights, where photopic/scotopic differences enter); this means that it’s necessarily many-to-one. Different spectra that generate the same response values are called metamers; metameric lights are interesting because, upon reflection by a surface, they can become nonmetamers (see Figure 28.21). In practice, most reflectance functions are nonspiky enough that metameric effects like this are not significant, although with LED lamps, which tend to have spikier spectra, the problem may be more serious.

The colors in the \(x+y+z=1\) plane of the CIE XYZ space are not all possible colors. As the sum \(x+y+z\) varies, other colors appear (such as maroon). Furthermore, colors like brown, which are generally used to describe reflective color rather than emissive color, tend not to appear at all.

The colors purple and violet are often considered to be synonymous, but violet is the name for a pure spectral color (at about 380 nm, just on the edge of perceptibility), while as we said, purple is the name for points on or near the straight bottom edge of the CIE horseshoe.

## 28.10 Intermezzo

Let’s pause and note the important points so far. First, color is a three-dimensional perceptual phenomenon evoked by the arrival of different spectral power distributions at the eye. Any color percept can be generated by a combination of the CIE primaries **X**, **Y**, and **Z**; if a color \(C\) is generated by \(XX + YY + ZZ\), we can think of \(X\), \(Y\), and \(Z\) as “coordinates” for that color in the space of all possible colors.

There are other coordinate systems on the space of colors, such as the CIE \(L^*u^*v^*\) and \(L^*a^*b^*\), in which \(L^*\) captures the notion of intensity, while the other coordinates encode chromaticity. In these systems, distances between color triples correspond to perceptual distances much more closely than do distances between \((X,Y,Z)\)-coordinate triples. But the coordinates in these systems are *not* linear functions of the \(X\), \(Y\), \(Z\)-coordinates (which are in turn linear functions of radiometric quantities), so they are not suitable for computations with a physical basis.

In both of the “perceptual” coordinate systems, there’s a free parameter, namely, the color chosen as “white.” Without the knowledge of the white point, you cannot convert an \(L^*u^*v^*\) coordinate triple into an \(XYZ\) triple, for instance.

We now move on from the description of color to the question of how to represent color in an image file, a television signal, etc. Considering that there’s only a half-century of experience in this regard, a surprisingly large number of representation methods have arisen.

## 28.11 White

As we mentioned earlier, many spectral power distributions appear white, so picking a particular white point can be a challenge. And an SPD that looks white at one intensity may look yellow at another intensity, because of the adaptation of the eye. Furthermore, the surroundings may have a substantial impact on the appearance of a color; if we watch a slide show in a dark room, showing a scene illuminated by incandescent lamps, we rapidly accommodate so that the white point of the slides appears white. But if that same slide show is shown in a well-lit room with white walls, the “white” within the slides may appear yellow, for instance.

The CIE has defined several standard “whites”; the simplest (from the point of view of computation) is illuminant \(E\), which has a constant SPD across the range of visible light. Illuminant \(C\), now deprecated but still widely used, attempts to approximate the white of sunlight. More common in modern usage are the \(D\) series of illuminants, which are tabulated by the CIE in 5 nm increments. Many of the most useful are, at a gross level, quite similar to blackbody distributions, and the names indicate this: D65 is similar to 6500 K black body radiation, D50 is similar to 5000 K radiation, etc. The photography industry uses the D55 standard; either this or D65 is a good choice for much of computer graphics.

## 28.12 Encoding of Intensity, Exponents, and Gamma Correction

As mentioned above, the CIE standard for defining \(L^*\) uses a 1/3-power law; the idea is that \(L^*\) is a reasonable measure of perceived brightness of light (at least within a modest range of luminances around the luminance of some reference white). Suppose that you wanted to store or transmit information about light without using too many bits. If you were engaged in physical measurements, you’d just want to choose some numeric representation of intensity. But if you were planning to use the information about light in some way that involved a human looking at it (e.g., if you were a television engineer trying to decide what information to encode in
