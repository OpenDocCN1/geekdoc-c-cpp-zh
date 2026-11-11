
and its weighted sum, using *w*, is 0.33. Notice that 0.33 is *not* 2.6 × .233 = .6058; in other words, computing the weighted sum and then multiplying is different from multiplying and then computing a weighted sum. Now imagine that *L* represents the light energy at five chosen frequencies, and *R* represents the reflectivity of a surface at those five frequencies. Then the term-by-term product represents the frequency distribution of the reflected light. But if we computed the weighted sum of each thing (i.e., the thing corresponding to the photometric measurements), then the product of the aggregate incoming light and the aggregate reflectivity is not the aggregate outgoing light. (There’s an argument to be made that we should not multiply the reflectances by the weights, but we should weight them evenly; even with this approach, commutativity fails.)

You may encounter other photometric terms; each of them can be thought of as a radiometric quantity, recorded per wavelength and then integrated against the luminous efficiency curve. Table 28.1 shows this correspondence.

*Table 28.1: Comparison of radiometric and photometric terms.*

| Concept | Radiometric Units | Photometric Units | Photometric Name (abbr.) |
|---|---|---|---|
| Spectral radiance | W m⁻² sr⁻¹ nm⁻¹ | lm m⁻² sr⁻¹ | Nit |
| … integrated over an area | W sr⁻¹ nm⁻¹ | lm sr⁻¹ | Candela (cd) |
| … integrated over a solid angle | W m⁻² nm⁻¹ | lm/m² | Lux (lx) |
| … integrated over an area and a solid angle | W nm⁻¹ | lm | Lumen (lm) |

Note that *radiance* is also an integrated form of spectral radiance, but it’s simply an integral over wavelength, without the weighting factor provided by the luminous efficiency curve. Because of this, you cannot compute photometric quantities from nonspectral radiometric quantities. If someone asks, “I’ve got a source that’s 18 W m⁻² sr⁻¹, how many nits is that?” there is no correct answer!

### 28.4.1.1 Scotopic and Photopic Vision

The rods (the other kind of receptor in the eye) are also sensitive to light, but in a different way than the cones. The cones are the dominant receptors in high-light situations (e.g., daytime), while the rods dominate in low-light situations (e.g., outdoors at night). The first of these is called *photopic* vision, and the second *scotopic* vision. The scotopic response curve is different from the photopic response curve (see Figure 28.7), having a peak at a lower wavelength and dropping to zero by about 650 nm. This means that the rods cannot detect the sort of light we perceive as “red.” Because both kinds of receptors perform some adaptation to average light levels, this makes red a good color for instruments that will be used in low-light situations: The red light from the instruments does not affect the average-light-level adjustment for the rods, which are the primary receptors in use for seeing things in the dark.

![](img/f464cd0043eb5336aa0543fe20a0561b_804_0.png)

*Figure 28.7: The luminous efficiency in photopic vision has a peak at 555 nm; the peak for scotopic vision is closer to 520 nm.*

### 28.4.1.2 Brightness

Our discussion so far has addressed the issue of how light of different wavelengths is perceived. There’s a separate issue: how light of different intensities (but constant spectral distribution) is perceived. In other words, if we have a diffuser—a piece of frosted glass, for example—and it can be lit from behind by 100 identical lamps, and we turn on one, or ten, or all 100 so that the diffuser appears to be a variable light source, how will our eyes and brains characterize the change in brightness? Given the wide range of intensities that we encounter in daily life, it’s hardly surprising that the response can be modeled as logarithmic: The change from one lamp to ten is perceived as being the same “brightness increase” as the change from ten lamps to 100. (Here we are using *brightness* in a purely perceptual sense, not as something physical to be measured, but as a description of a sensation.) That is to say, this model says that the perceptual strength associated to seeing a light of luminous intensity *I* is

$$S = k \log(I). \tag{28.8}$$

In support of the idea of a logarithmic model of our sensitivity to luminance, we can display two lights of the same luminous intensity and then adjust one until it becomes just noticeably different from the other. By doing this over and over at different starting sensitivities, we find that the **just noticeable difference** (or **JND**) is about 1% (i.e., 1.01*I* is noticeably different from *I*) for a wide range of intensities. In very dark and very bright environments, the number increases substantially, but for a range that includes the intensity ranges of virtually all of today’s displays, it is about 1%. So if we adjusted the intensity repeatedly by 1%, we might expect to say that the brightness had increased by several “steps,” and that *k* steps of increase would be achieved by multiplying by (1.01)^k. (This reasoning makes the assumption that each JND seems to the viewer to be of the same “size,” however.) This implies that the response is proportional to the logarithm of the intensity.

An alternative model (Stevens’ law) says that the response should be modeled by a power law:

$$S = cI^b, \qquad (28.9)$$

where $b$ is a number slightly less than 1. The shapes of the graphs of log and $y = x^b$ are somewhat similar—both concave down, both slowly growing—so it’s no surprise that both can be used to fit the data decently. Each model has its detractors, but from our point of view, the important feature is that either one can be used to generate a good fit to the data, *particularly* when the range of brightnesses being considered is relatively small. In fact, as we’ll discuss later, the eye adapts to the prevailing light in an environment, and intensities that differ from this by modest amounts can be compared to one another. But our sensation of lights that are very bright or very dim compared to the average is quite different (“too dark to see” or “too bright to look at”).

The Commission Internationale de l’Éclairage (CIE), a group responsible for defining terms related to lighting and color, chose to use a modified version of Stevens’ law to characterize perceptual responses to light, and it’s this model that we’ll use in further discussing the perception of brightness. To be explicit, the CIE defines **lightness** as

$$L^* = \begin{cases}116(Y/Y_n)^{1/3} - 16 & \frac{Y}{Y_n} > 0.008856 \\ 903.3(Y/Y_n) & \frac{Y}{Y_n} \le 0.008856\end{cases}, \qquad (28.10)$$

where $Y$ (called **luminance**) denotes a CIE-defined quantity that’s proportional (for any fixed spectrum) to the energy of the light, and $Y_n$ denotes the $Y$ value for a particular light that you choose to be the “reference white.”

You can see that $L^*$ is defined by a 1/3 power law that’s been shifted downward a little (the −16 does this), and which has had a short linear segment added to deal with very low light values. In practice, this linear segment applies only to intensities that are a factor of more than 100 smaller than that of the reference white; in a typical computer graphics image, these are effectively black, so the linear segment is mostly irrelevant.

In practice, this logarithmic or power-law nature of things is somewhat confounded by “adaptation” of the rods and cones. The luminance we encounter in ordinary experience ranges over a factor of $10^9$ between a moonless overcast night and a snowy region on a sunny day. Both rods and cones react to arriving light with chemical changes, which in turn generate an electrical change that is communicated to the brain. Plotting the output of the various sensors against the log of the luminance, we get a graph like the one shown in Figure 28.8: the rods react to varying luminance by changing their output … up to a point. After that point, any further increase in luminance doesn’t affect the rods’ output, and they are said to be **saturated**. The cones, on the other hand, begin to change their output substantially at about that point, so differences in brightness are detected by the photopic system. The placement of the cones’ curve on the axes, though, is not fixed: Upon exposure to light of a certain level, like $D$ on the chart, the cones, which were near the limit of their output, will gradually *adapt* and shift their response curve so that it’s centered at $D$, thus responding to light changes at or near $D$. This ability to adapt is limited—at some point, all light begins to seem “very bright.” The function of the “reference white” in the CIE definition is to characterize the interval of intensities over which we want to characterize lightness.
