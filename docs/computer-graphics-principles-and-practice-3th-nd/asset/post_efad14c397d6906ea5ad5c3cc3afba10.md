
characteristics is a matter of choice (just as choosing the coordinate axes to use on a plane is a matter of choice; any pair of perpendicular lines can work!). So some people choose to describe colors in terms of hue, saturation, and “value,” while others prefer to describe mixes of red, green, and blue. We’ll say much more about these in Section 28.13.

Careful physiological experiments have revealed much of the structure of the eye; Deering [Dee05] presents a good summary of the results of this work in the context of understanding what the retina can detect, which provides a guide to what is worth rendering in the first place. The key thing, from the point of view of understanding color, is the presence of two kinds of receptors: **rods** and **cones**. Rods are sensitive to visible light of all wavelengths, while the three types of cones are sensitive to different wavelengths of light: The first has its peak response at 580 nm, the second at 545 nm, and the third at 440 nm (see Figure 28.4). Detailed observations of the response curves for the receptors (including rods) are described by Bowmaker and Dartnall [BD80]. These are often described as “red,” “green,” and “blue” receptors, even though the red and green peaks occur at wavelengths commonly described as yellow, with the red peak being an orangey yellow and the green peak being a greener yellow. (To be more precise, a monochromatic light of 580 nm wavelength causes, in most viewers, the percept “orangey yellow.”) A better set of names is “long wavelength,” “medium wavelength,” and “short wavelength” receptors, and the names \(L\), \(M\), and \(S\) are often used for these. We’ll generally use “red,” “green,” and “blue,” however, to avoid the need to convert from wavelength to color.

![](img/f464cd0043eb5336aa0543fe20a0561b_799_0.png)

*Figure 28.4: The approximate spectral response functions of the three types of cones in the human retina; the labels R, G, and B are misleading, because the peaks of the R and G curves both correspond to monochromatic lights that most people describe as in the “yellow” range.*

One can read this graph by saying, for instance, that a certain amount \(e\) of light at 560 nm will cause a response in a red receptor, but that one would need twice as much light at wavelength 530 nm to generate the same response in that red receptor. (Of course, these lights provoke very different responses in the green and blue receptors, too.) Furthermore, the effects of different lights on the red receptor are additive: Sending in both \(e\) light at 560 nm and \(2e\) light at 530 nm will generate the same red-receptor response as sending \(2e\) at 560 nm. If we use \(f(\lambda)\) to indicate the red receptor’s response at wavelength \(\lambda\) and use \(I(\lambda)\) to indicate the incoming light’s intensity at wavelength \(\lambda\), then the total response from the receptor will be

$$\int_{400\,\text{nm}}^{700\,\text{nm}} I(\lambda) f(\lambda)\,d\lambda. \tag{28.2}$$

In short, the total response is a linear function of the incoming light *I*, with the linear operation being “integrate against the response curve.”

With this in mind, we can consider a system diagram (see Figure 28.5) tracing how a physical phenomenon (the spectral power distribution of light) becomes a perceptual phenomenon (the experience of color). Notice that this diagram is slightly simplified, in that it treats the incoming light without considering how the pattern of light is organized (i.e., what the person is actually seeing). This omission makes it impossible for this model to account for phenomena like spatial comparison of colors or color constancy, but the simplification—we can imagine that all the light arriving comes from a single, large, glowing surface surrounding the viewer—makes it easy to discuss the basic phenomena of color.

![](img/f464cd0043eb5336aa0543fe20a0561b_800_0.png)

*Figure 28.5: Light, described by its spectral power distribution, enters the eye; the three types of cones each respond and their individual responses are conducted by the optic nerves to the brain, resulting in a perception of color. These correspond to three distinct areas of study: physics, physiology, and perceptual psychology.*

## 28.4 The Perception of Color

Given the three types of cones, it’s not surprising that color perception appears to be three-dimensional. We begin with the examination of the aspect that’s least related to color, which is **brightness**—the impression we have of how bright a light is, independent of its hue. By the way, the brightness we are referring to is not a quantity that has physical units; it’s a generic and informal term used to characterize the human sensation of the amount of light arriving at the eye from somewhere (a lamp, a reflecting surface, etc.).

### 28.4.1 The Perception of Brightness

To determine relative brightness of light at different wavelengths, imagine an experiment in which you are shown two lights: a 555 nm reference monochromatic light source, and a second monochromatic light source whose wavelength \(\lambda\) will be varied over the range 400 nm to 700 nm. We fix a particular wavelength \(\lambda\), and you are given a knob with which you can control a multiplier for the reference light source; you adjust it until it has the same brightness as the one at wavelength \(\lambda\). We record the setting \(g(\lambda)\) and reset \(\lambda\) to a new value and repeat. When we are done, we have a tabulation of how effective light at wavelength \(\lambda\) is at seeming bright, compared to light at the reference wavelength 555 nm. For each value of \(\lambda\), the number \(g(\lambda)\) tells how much less effective light at wavelength \(\lambda\) is in provoking a response than light at wavelength 555 nm. Scaling so that the largest value of \(g(\lambda)\) is 100%, we can plot the resultant function \(\lambda \mapsto e(\lambda)\) (see Figure 28.6); the resultant graph shows the **luminous efficiency function** for the human eye. (“Efficiency” here refers to how efficient energy at a particular wavelength is in provoking the sensation of brightness.)

![](img/f464cd0043eb5336aa0543fe20a0561b_801_0.png)

*Figure 28.6: The luminous efficiency at each wavelength tells how much less bright light of that wavelength appears than light at the standard wavelength of 555 nm.*

The luminous efficiency graph actually varies from person to person, and varies based on the person’s age as well; in view of this, a standard luminous efficiency curve was derived by averaging many observations.

This standardized tabulation can be used to define the **luminance** of a light source: We multiply the intensity at each of the tabulated wavelengths by the luminous efficiency value for that wavelength, and compute the sum, thus approximating the value

$$\int I(\lambda)e(\lambda)\,d\lambda, \tag{28.3}$$

where \(I(\lambda)\) is the spectral intensity at wavelength \(\lambda\). The resultant value has units of **candelas**, which is the SI unit for the measurement of **luminous intensity**. One candela is the luminous intensity, in a given direction, of a source that emits monochromatic radiation at a frequency of \(540 \times 10^{12}\) Hz (i.e., 555 nm wavelength),$^1$ and whose radiant intensity in that direction is 1/683 watt per steradian. The international standards committee chose the peculiar numbers in this definition to make it closely match earlier measurements that were based on the light from a single standard candle, or the light from a certain near-blackbody source (a square centimeter of melting platinum). Naturally, light at other wavelengths, of equal radiant intensity, produces fewer candelas of visible light than does light at 555 nm.

To give a sense of common illumination in terms of candelas, my LCD screen emits about 250 candelas per square meter (one candela per square meter is called a **nit**; it’s the photometric term corresponding to radiance in radiometry), while the light from the screen at a movie theatre is about 40 candelas per square meter.

1. The definition is given in terms of frequency rather than wavelength because the speed of light varies in different media; in graphics, where we work primarily with light in air, this consideration is irrelevant.
