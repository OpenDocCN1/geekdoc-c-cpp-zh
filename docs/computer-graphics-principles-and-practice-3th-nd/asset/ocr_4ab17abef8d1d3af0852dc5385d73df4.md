the area. The cosine term also varies from point to point for an area source but is constant for the omni-light’s point source; one might say that this is another way that size “matters.” Regardless, the conclusion is that we can use exactly the same formula for the radiance from area and point sources.

The irradiance at $P$ due to the omni-light at $Q$ (see Figure 14.31) is given by

$$M_i(Q,P)=\frac{\Phi}{4\pi\,\|Q-P\|^2\,\mathrm{sr}}\tag{14.39}$$

if there is no scene point on the open line segment from $Q$ to $P$; it is 0 if there is an occlusion.

Note that we could say that the effective radiance is

$$L(P,-\omega_i)=\frac{\Phi}{4\pi\,\mathrm{sr}\,\|Q-P\|^2}\tag{14.40}$$

that is, it is proportional to the total power of the luminaire and falls off with the square of distance from the luminaire. In fact, if we were to insert that expression into a renderer it would yield the desired image so long as $\|Q-P\|$ was “sufficiently large.” However, this is not actually a true radiance expression because it is not conserved along a ray—it falls off with distance because our omni-light in fact has the physically impossible zero surface area, which leads it to create a physically impossible radiance field in space. Note that both the radiance and the irradiance approach infinity as $\|Q-P\|\to 0$. It is common practice to clamp the maximum irradiance from an omni-light, since when that distance is small our original assumption that the distance to the luminaire is much greater than the size of the luminaire is violated and the resultant estimated light intensity is greater than intended. A less efficient but more accurate correction would be to actually model the luminaire as an object with nonzero surface area (such as a sphere) when the distance is less than some threshold.

There is no illumination from the omni-light at locations that do not have an unobstructed line of sight. These regions form the shadows in an image. The boundary of the shadows from an omni-light will be “hard,” with a distinct curve across a surface that distinguishes it from shadowed. This is unlike the area sources, which produce “soft” shadows with blurry silhouettes. A lighting algorithm such as shadow mapping that evaluates light visibility at lower precision than the radiance magnitude can appear to produce soft shadows from a point light. This is in fact an artifact of reconstruction from an aliased set of samples. Nonetheless, it may be visually pleasing in practice.

![](bbox=[0.706, 0.125, 0.909, 0.207])

Figure 14.31: Points and directions in point-light equations.

# 14.11.7 Directional Light

For an omnidirectional point light that is far from all locations in the scene, $\omega_i$ and $L(P,-\omega_i)$ due to the light vary little across the scene. A **directional light** is an omni-light with the further simplifying approximation that it is so far from the rest of the scene that $\omega_i$ and $L$ can be treated as constant throughout the scene. This eliminates some of the precision and modeling challenges of placing a point light very far away, while giving a reasonable model for a distant light source such as the sun.

We could model the total power of the distant point light, but it is typically enormous and “distant” is ambiguous, so it is easier to model the (constant) incident radiance at points in the scene by simply letting $L(P,\omega)=L_0$ for $\omega_i$ directed