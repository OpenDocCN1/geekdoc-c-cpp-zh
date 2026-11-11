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

# 28.4.1.1  Scotopic and Photopic Vision

The rods (the other kind of receptor in the eye) are also sensitive to light, but in a different way than the cones. The cones are the dominant receptors in high-light situations (e.g., daytime), while the rods dominate in low-light situations (e.g., outdoors at night). The first of these is called *photopic* vision, and the second *scotopic* vision. The scotopic response curve is different from the photopic response curve (see Figure 28.7), having a peak at a lower wavelength and dropping to zero by about 650 nm. This means that the rods cannot detect the sort of light we perceive as “red.” Because both kinds of receptors perform some adaptation to average light levels, this makes red a good color for instruments that will be used in low-light situations: The red light from the instruments does not affect the