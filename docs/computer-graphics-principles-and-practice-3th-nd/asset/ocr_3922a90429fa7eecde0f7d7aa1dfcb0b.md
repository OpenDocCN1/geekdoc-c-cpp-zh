![](bbox=[0.212, 0.108, 0.553, 0.323])

*Figure 28.16: The color-matching functions, which indicate, for each wavelength, how much of a standard red, green, and blue light must be mixed to produce the same sensor responses as a monoespectral light of wavelength λ. At least one mixing coefficient is negative for many monospectral lights, indicating the impossibility of making those colors as mixes of red, green, and blue.*

and use these as the amounts of our red, green, and blue primaries. (Of course, if any of the three computed coefficients is negative, we cannot reproduce the color with our sources.)

Unfortunately, the set of all convex combinations of our three primaries doesn’t include all possible colors; geometrically, the triangle whose vertices correspond to our primaries is a proper subset of the horseshoe-shaped set of sensor responses.

In 1931, the CIE defined three standard primaries, which it called **X, Y, and Z**, with the property that the triangle with these three as vertices actually includes all possible sensor responses. To do so, the CIE had to create primaries that had *negative* regions in their spectra, that is, they did not correspond to physically realizable light sources. Nonetheless, these primaries have certain advantages.

+   - The **Y** primary was defined so that its color-matching function was exactly the luminous efficiency curve; this means that for any spectral light source, *T*, written as a combination
+   
+     *T = cₓX + cᵧY + c_zZ,* (28.16)
+   
+     the number *cᵧ* will be the perceived intensity of the light. This was significant in developing black-and-white televisions: The signal had to transmit in some form the *Y*-component of the lights that the camera was seeing. Later, when color signals began to be broadcast, the *cₓ* and *c_z* data were sent in a different band; color televisions could decode these, and black-and-white televisions could ignore them.

+   - The color-matching functions for **X, Y, and Z** are everywhere non-negative (see Figure 28.17), so all colors are expressed as non-negative linear combinations of the primaries.

2. The value *cᵧ* itself is not what’s transmitted; more on this later.