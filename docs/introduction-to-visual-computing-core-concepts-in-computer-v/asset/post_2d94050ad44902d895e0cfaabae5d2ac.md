
different directions as they are illuminated from different directions. Painters and photographers have for centuries explored the appearance of trees and urban areas under a variety of conditions, accumulating knowledge about “how things look” – which is nothing but BRDF related knowledge.

So, let us now define BRDF at a surface point P formally. Let us consider a point on a surface P with a normal n, illuminated from a direction k_i. This is achieved by placing a light source in this direction. Let the irradiance incident at P be H. Let the radiance going out towards a viewing direction k_o be L_s. This setup is illustrated in Figure 9.1. The BRDF ρ is defined as the ratio of L_s to H, i.e.

```
ρ(k_i, k_o) = L_s / H.  (9.12)
```

Therefore, BRDF gives us the fraction of light exiting towards the viewing direction k_o when illuminated from the incident direction k_i. Note that both k_o and k_i are directions in 3D and can be represented with two angles in spherical coordinate. Let k_i be given by (θ_i, φ_i) and k_o be given by (θ_o, φ_o). Therefore, BRDF is a four dimensional function ρ(θ_i, φ_i, θ_o, φ_o). Also, note the ρ is a ratio of radiance by irradiance. Therefore its unit is (sr)^{-1}.

Directional Hemispherical Reflectance Let us consider a simple question, “What fraction of the incident light is reflected?”. It is evident that this number should be between 0 to 1 purely from the standpoint of conservation of energy. Let us now see if this question can be easily answered using BRDFs. Given an incident light from the direction k_i, the fraction that is reflected should be the ratio of outgoing irradiance (or radiance exitance) to the incoming irradiance. Therefore, the directional hemispherical reflectance for the D(k_i) is given by the ratio of radiance exitance E to irradiance H as

```
D(k_i) = E / H.  (9.13)
```

From Equation 9.12 we know that

```
L_s(k_o) = H ρ(k_i, k_o)  (9.14)
```

Also, from the definition of radiance in Equation 9.8 we know that

```
L_s(k_o) = ΔE / (Δσ_o cosθ_o).  (9.15)
```

Therefore,

```
H ρ(k_i, k_o) = ΔE / (Δσ_o cosθ_o).  (9.16)
```

Rearranging terms we get the contribution of E/h reflected in the direction of k_o as

```
ΔE / H = ρ(k_i, k_o) Δσ_o cosθ_o  (9.17)
```

Therefore,

$$D(\mathbf{k_i}) = \frac{E}{H} = \int_{\forall \mathbf{k_o}} \rho(\mathbf{k_i},\mathbf{k_o}) cos\theta_o d\sigma_o \tag{9.18}$$

An ideal diffuse surface is called *Lambertian* and is considered to have a constant BRDF at any viewing direction. In other words, the appearance of the object is view-agnostic or view-independent. Though such surfaces are practically non-existent, many objects with *matte* appearance are often modeled as a Lambertian surface. Let us consider such a Lambertian surface with $\rho = C$. Then the directional hemispherical reflectance of such a surface is given by

$$D(\mathbf{k_i}) = \int_{\forall \mathbf{k_o}} C \Delta\sigma_o cos\theta_o d\sigma_o \tag{9.19}$$ $$= \int_{\phi_o=0}^{2\pi} \int_{\theta_o=0}^{\frac{\pi}{2}} C \ cos\theta_o \ sin\theta_o \ d\theta_o \ d\phi_o \tag{9.20}$$ $$= \pi C \tag{9.21}$$

Therefore, if we consider a perfectly reflecting Lambertian surface where $D(\mathbf{k_i}) = 1$, then its BRDF is $\frac{1}{\pi}$.

## 9.1.2 Light Transport Equation

Using the aforementioned equations, we can now write a simple light transport equation that defines how light is transported via surfaces or objects in the presence of lights from many different directions. If we consider radiance $L_i$ from the direction $\mathbf{k_i}$ along a small solid angle $\Delta\sigma_i$, the irradiance due to this light is given by $L_i cos\theta_i \Delta\sigma_i$ where $\theta_i$ is the angle between $\mathbf{k_i}$ and $\mathbf{n}$. Therefore, the outgoing radiance $\Delta L_o$ in the direction $\mathbf{k_o}$ due to the radiance coming in from direction $\mathbf{k_i}$ is given by

$$\Delta L_o = \rho(\mathbf{k_i},\mathbf{k_o}) L_i cos\theta_i \Delta\sigma_i \tag{9.22}$$

Therefore, to consider the radiance from all the different directions (all different values of $\mathbf{k_i}$), the total irradiance in the direction of $\mathbf{k_o}$ is given by

$$L_s(\mathbf{k_o}) = \int_{\forall \mathbf{k_i}} \rho(\mathbf{k_i},\mathbf{k_o}) L_f(\mathbf{k_i}) cos\theta_i d\sigma_i \tag{9.23}$$

This is called the rendering equation or light transport equation and is the cornerstone of building illumination models, simple or complex.

## 9.2 Photometry and Color

For every radiometric property, there is a corresponding photometric property that intuitively measures "how much of it can the human observer make use of".

![](img/66c45bbed85bb7ba7f7b05dff49b5060_222_0.png)

Figure 9.2. This figure shows the visible spectrum of light and its position with respect to the invisible spectrum.

Therefore, photometric quantities have an aspect of perception associated with them. Color is a photometric quantity that we use all the time. It is a part and parcel of our lives, so much so, that we probably cannot appreciate it unless we lose our perception of color. Mr. I, who lost color perception due to an accident exclaimed with anguish, “My dog looks gray, tomato juice is black and color TV is an hodge podge”. Color not only adds beauty to our life, but serves important signaling functions. The natural world provide us with many signals to identify and classify objects. Many of these come in terms of color. For e.g. banana turns yellow when its ripe, the sky turns red when it is dawn and so on.

The color stimuli is the radiometric quantity (usually radiance), that reaches the human eye from any point in the world. The important parameter in the context of photometry, and therefore color vision, is the associated wavelength λ. The visible light spectrum has wavelength that varies between 400 nm and 700 nm. Figure 9.2 shows the visible spectrum of colors. A illumination or an object selectively emit or reflect respectively certain wavelengths more than other. Two things are responsible for our color vision and hence photometry. The first is the selective reflection of wavelengths by different objects. However, it is only one of the factors responsible for the color of an object. The second important factor is the eye’s selective response to different wavelengths. This response, and hence the perception of color, can be different from species to species, and also shows a variance across individuals of the same species. That is the reason, color is often considered as a perception, and not reality!

Let us start from the illumination of a scene. A scene is usually lighted by

![](img/66c45bbed85bb7ba7f7b05dff49b5060_223_0.png)

Figure 9.3. Left: The illumination spectrum (I(λ)) of a flouroscent (bold line) and tungsten lamp (dotted line). Right: The reflectance spectrum (R(λ)) of a red apple.

some light source. This light source emits light differently at different wavelengths λ. This function, denoted by I(λ) gives the illumination spectrum. Similarly, for an object, its relative reflectance at different wavelengths define its reflectance spectrum R(λ). Since the reflectance or reflectivity of an object is the ratio of outgoing to incoming power, it is between 0 and 1 for an object that is not a light source. These spectra for a couple of light sources and a red apple are illustrated in Figure 9.3.

When an object is illuminated by a light source, the amount of light that is reflected from that object at different wavelengths is given by the product of I(λ) and R(λ). Since this is the spectrum that stimulates the vision, this is called the color stimuli or color signal, denoted by C(λ). Thus,

C(λ) = I(λ) × R(λ)  (9.24)

as illustrated in Figure 9.4. The physical quantity we are dealing with here is power per unit area per unit solid angle per unit wavelength (W m⁻¹ (nm)⁻¹ (sr)⁻¹). Therefore, we are essentially thinking of radiance when we are defining the color stimuli.

Color stimuli can be of different types as shown in Figure 9.4. When it has light of only one wavelength, it is called monochromatic, e.g. a laser beam. When the relative amount of light from all wavelengths is equal, then it is called achromatic. The sunlight is close to achromatic in the day time. Finally, if the stimulus has different amounts of light from different wavelengths, it is called polychromatic. Most of the time we deal with polychromatic light. Most of the manmade and natural color stimuli are smooth spectra of polychromatic light.
