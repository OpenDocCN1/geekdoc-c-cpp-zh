![](bbox=[0.145, 0.105, 0.555, 0.272])

*Figure 28.6: The luminous efficiency at each wavelength tells how much less bright light of that wavelength appears than light at the standard wavelength of 555 nm.*

provoking a response than light at wavelength 555 nm. Scaling so that the largest value of $g(\lambda)$ is 100%, we can plot the resultant function $\lambda \mapsto e(\lambda)$ (see Figure 28.6); the resultant graph shows the **luminous efficiency function** for the human eye. (“Efficiency” here refers to how efficient energy at a particular wavelength is in provoking the sensation of brightness.)

The luminous efficiency graph actually varies from person to person, and varies based on the person’s age as well; in view of this, a standard luminous efficiency curve was derived by averaging many observations.

This standardized tabulation can be used to define the **luminance** of a light source: We multiply the intensity at each of the tabulated wavelengths by the luminous efficiency value for that wavelength, and compute the sum, thus approximating the value

$$\int I(\lambda)e(\lambda)\,d\lambda, \tag{28.3}$$

where $I(\lambda)$ is the spectral intensity at wavelength $\lambda$. The resultant value has units of **candelas**, which is the SI unit for the measurement of **luminous intensity**. One candela is the luminous intensity, in a given direction, of a source that emits monochromatic radiation at a frequency of $540 \times 10^{12}$ Hz (i.e., 555 nm wavelength),$^1$ and whose radiant intensity in that direction is 1/683 watt per steradian. The international standards committee chose the peculiar numbers in this definition to make it closely match earlier measurements that were based on the light from a single standard candle, or the light from a certain near-blackbody source (a square centimeter of melting platinum). Naturally, light at other wavelengths, of equal radiant intensity, produces fewer candelas of visible light than does light at 555 nm.

To give a sense of common illumination in terms of candelas, my LCD screen emits about 250 candelas per square meter (one candela per square meter is called a **nit**; it’s the photometric term corresponding to radiance in radiometry), while the light from the screen at a movie theatre is about 40 candelas per square meter.

1. The definition is given in terms of frequency rather than wavelength because the speed of light varies in different media; in graphics, where we work primarily with light in air, this consideration is irrelevant.