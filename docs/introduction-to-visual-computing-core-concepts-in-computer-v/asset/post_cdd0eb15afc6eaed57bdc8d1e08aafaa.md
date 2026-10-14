
## Exercises

- 4. Consider a camera attached to the front of the car as it is traversing on a straight bridge, the end of which is marked with a conspicuous building and the sides containing landmark paintings hanging from the bridge at equal intervals which is known. Consider two pictures taken from this camera. Which 3D scene location would appear at the focus of expansion? Assuming that you can detect the amount each landmark painting has moved from one picture to another, how can you find the speed of the car?

- 5. Consider a scene which is constant being observed by a pair of frontal stereo cameras. If the baseline of the camera is increased, how would the disparity of the 3D points change in the images captured? Justify your answer.

- 6. Suppose we would like to determine the size of a cube from a set of $k$ calibrated cameras whose extrinsics are unknown (but whose intrinsics are known). Suppose each of the cameras can see the same $m$ corners of the cube, and suppose there is no correspondence problem. How many cameras and how many corners do we need to determine the size of the cube? (Notice: a cube has only 8 corners, hence $m \leq 8$). If multiple solutions exist, give them all. If no solution exists, explain why.

## Part IV

## Radiometric Visual Computing

![](img/66c45bbed85bb7ba7f7b05dff49b5060_216_0.png)

Taylor & Francis
Taylor & Francis Group
http://taylorandfrancis.com

## Light

In this chapter we will discuss the science of light, more commonly termed as radiometry. We will discuss different radiometric quantities and how they are used in the domain of visual computing. Then we will see how radiometry leads to photometry which is the science of light in the context of the human visual system and hence human perception.

### 9.1 Radiometry

In radiometry light is considered to be a traveling form of energy and therefore the unit used to describe it is the SI unit of energy, joule (J). This energy is associated with a source of origin, which is usually defined by its position, a direction of propagation and a wavelength λ. This conforms to the particle theory of light where the smallest unit of light is considered to be a photon or a quantum of energy. This also conforms to the wave theory of light, which assumes light to be a waveform traveling in a particular direction. λ is expressed by units of nanometers (nm). Light travels with a speed cₙ in a medium of refractive index n. An invariant in this context is the frequency f of light is given by

f = cₙ / λ
(9.1)

which does not change unlike cₙ and λ. Another invariant is the energy carried by a photon,

q = h c / λ
(9.2)

where h = 6.63 × 10⁻³⁴ J is the Planck’s constant.

The spectral energy is a density function that gives the density of the quantum energy at an infinitesimal interval of wavelengths around λ with a width of Δλ. Note that due to the particle nature of light, spectral energy at a wavelength is a quantum value (either 0 or non-zero), but its density in an interval of wavelengths can be defined in a non-quantum fashion. This is similar to population where population at any point in space is either existent or non-existent, but the density

of population over an area is always a non-quantum quantity. Just like population density, it is better to view the spectral energy which is a continuum and does not become granular even when the area is small. Therefore, spectral energy ΔQ is defined as

```
ΔQ = Δq / Δλ
```

and has the unit of J(nm)⁻¹.

However, we are more interested in spectral power that is defined as the spectral energy over infinitesimal time Δt. It is given by ΔQ/Δt and has the unit of W(nm)⁻¹. Imagine a camera that leaves its shutter open for Δt time and has a filter of Δλ. Such a sensor would measure the spectral power.

Irradiance, H, is defined as the spectral power per unit area and is given by

```
H = Δq / (ΔA Δt Δλ)
```

where ΔA can be considered as the finite area of the sensor measuring the spectral power, assuming that the sensor is parallel to the surface being measured. The unit of irradiance is therefore W m⁻²(nm)⁻¹ or J s⁻¹ m⁻²(nm)⁻¹. Irradiance is usually used to define the amount of spectral power incident or hitting a unit area. When the same quantity is used in the context of amount of spectral power leaving or reflected off a unit area, it is often called radiant exitance, E.

Irradiance only tells us about how much light hits a point, but it does not say much about the direction the light is coming from. Therefore, irrandiance can be considered to be the quantity measured by the sensor when a conical light limiter is placed on the sensor to limit the direction of the light it is measuring to Δσ. Therefore, radiance is defined as irradiance per unit direction as

```
R = ΔH / Δσ = Δq / (ΔA Δt Δλ Δσ)
```

and is measured by the unit W m⁻²(nm)⁻¹(sr)⁻¹ or J s⁻¹ m⁻²(nm)⁻¹(sr)⁻¹ where sr stands for steridian, the SI unit for a solid angle. It is analogous to radians used to define planar angles. A useful property of radiance is that it does not vary along a line in space. Consider the sensor with a conical light limiter of angle σ measuring the light hitting a surface from a distance d. Let the circular area subtended by this cone be ΔA. If we increase the distance by a factor of k to kd, the area being measured by the detector will increase by k² but the light reaching the detector will be attenuated by the same factor k² (due to distance attenuation of light being inversely proportional to the distance) thereby keeping the radiance constant. Here we consider the sensor to be parallel to the surface whose radiance is being considered. In other words, the normal to the surface is perpendicular to the sensor. However, the more general situation is when the sensor is titled by an angle θ. In this case, the area sampled by the detector will

no longer be a circle but an ellipse with a larger area of $\Delta A\cos(\theta)$. Therefore, radiance will be defined by

$$R=\frac{\Delta H}{\Delta\sigma}=\frac{\Delta q}{\Delta A\cos\theta\Delta t\Delta\lambda\Delta\sigma}. \tag{9.6}$$

As with irradiance, it is important to distinguish between the radiance incident from a point on the surface and radiance exiting from a point of the surface. The former is called *field radiance*, $L_f$, and the latter is called *surface radiance*, $L_s$. Therefore,

$$L_s=\frac{\Delta E}{\Delta\sigma\cos\theta} \tag{9.7}$$
$$L_f=\frac{\Delta H}{\Delta\sigma\cos\theta} \tag{9.8}$$

![](img/66c45bbed85bb7ba7f7b05dff49b5060_219_0.png)

The reason radiance is considered to be the most fundamental radiometric quantity is that if we know $R_f$ of a surface, we can derive all the other radiometric quantities from there. For example, irradiance can be expressed from the field radiance as

Figure 9.1. This figure shows the surface point $P$ with normal $n$ and the incident light direction $k_i$ and viewing direction $k_o$ for the BRDF $\rho(k_i,k_o)$ at $P$.

$$H=\int_{\mathcal V}L_f(k_i)\cos\theta\,d\sigma \tag{9.9}$$

where $k_i$ is an incident direction that can be expressed as a $(\theta,\phi)$ pair in the spherical coordinate system with respect to the normal at that point on the surface and is associated with a differential solid angle $d\sigma$. For example, if $L_f$ is constant across all directions, we can compute the irradiance by replacing $d\sigma=\sin\theta\,d\theta\,d\phi$ as

$$H=\int_{\phi=0}^{2\pi}\int_{\theta=0}^{\pi/2}L_f\cos\theta\sin\theta\,d\theta\,d\phi \tag{9.10}$$
$$=\pi L_f \tag{9.11}$$

Note the constant $\pi$ will appear in many radiometric calculations and is the artifact of how we measure solid angles. We consider the area of the unit sphere to be a multiple of $\pi$ rather than multiple of one. Similarly we can compute the spectral power incident on a surface by finding $\int_{\mathcal V_x}H(\mathbf{x})\,dA$ where $\mathbf{x}$ is a point of the surface associated with a differential area of $dA$.

### 9.1.1 Bidirectional Reflectance Distribution Function

Bidirectional Reflectance Distribution Function or BRDF is a formal way to describe what we humans face everyday – objects look different when viewed from
