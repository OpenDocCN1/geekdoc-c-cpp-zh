For a solid-color material, the innate colors for the diffuse and specular layers are constant across a surface. For a textured material, the texture image and texture algorithm together determine the diffuse-layer color at each individual surface point.

The three efficiency factors are each expressed as an RGB triple, with each entry being a number between 0 and 1, with 0 meaning “no efficiency” and 1 meaning “full efficiency.” For example, we would specify \(k_{a,R} = 0.5\) for a diffuse layer that reflects exactly half of the red component of the ambient light in the scene.

What we’ve called “reflection efficiency” here is closely related to the physical notion of reflectivity, which we’ll examine in detail in Chapter 26.

Next, let’s examine the inputs that are specified by or derived from the lights that have been placed in the scene, via any of WPF’s light-specification elements, such as `DirectionalLight`:

| Symbol | Description | Format |
|---|---|---|
| \(I_a\) | Color/intensity of the scene’s ambient light | \((I_{a,R}, I_{a,G}, I_{a,B})\) |
| \(I_{dir}\) | Color/intensity of a directional light source | \((I_{dir,R}, I_{dir,G}, I_{dir,B})\) |
| \(I_{geom}\) | Color/intensity of a geometric light source | \((I_{geom,R}, I_{geom,G}, I_{geom,B})\) |
| \(F_{att}\) | Attenuation factor for geometric lights | a single real number |

A geometric light’s actual contribution is subject to attenuation. The attenuation factor \(F_{att}\) is calculated for each surface point \(P\), based on the light’s characteristics and distance from \(P\). Thus, the actual light arriving at the surface point \(P\) from the geometric light source is

\[
(F_{att} I_{geom,R};\ F_{att} I_{geom,G};\ F_{att} I_{geom,B}).
\]

Now that we have enumerated all of the inputs, we are ready to examine the WPF lighting equation. Here is the equation that computes the intensity of the red light that reaches the camera from a specific surface point (we examine each component in detail below):

\[
\begin{aligned}
I_R ={} & (I_{a,R}\ k_{a,R}\ C_{d,R}) \\[-2pt]
&+ \sum_{\text{directional lights}} (I_{dir,R}\ k_{d,R}\ C_{d,R}\ (\cos\theta)) \\[-2pt]
&+ \sum_{\text{geometric lights}} (F_{att}\ I_{geom,R}\ k_{d,R}\ C_{d,R}\ (\cos\theta)) \\[-2pt]
&+ \sum_{\text{directional lights}} (I_{dir,R}\ k_{s,R}\ C_{s,R}\ (\cos\delta)^s) \\[-2pt]
&+ \sum_{\text{geometric lights}} (F_{att}\ I_{geom,R}\ k_{s,R}\ C_{s,R}\ (\cos\delta)^s)
\end{aligned}
\]
(6.2)–(6.7)

The sums in the equations above are over all lights of various kinds, which we’ll describe shortly.

If the scene contains multiple lights, and/or if the material uses multiple components (e.g., both ambient and diffuse) with high reflection efficiency coefficients, the computed result may be greater than 100% intensity, which has no