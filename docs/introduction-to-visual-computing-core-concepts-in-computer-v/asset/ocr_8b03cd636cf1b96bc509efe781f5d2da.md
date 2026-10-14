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