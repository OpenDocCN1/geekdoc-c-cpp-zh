rather than one; so does topaz. (That’s because the speed of light is different in different directions through these materials!)

# 26.5.1 Radiance Computations and an “Unpolarized” Form of Fresnel’s Equations

While Fresnel’s laws describe transmitted and reflected power, in graphics we’re mostly concerned with radiance, which we’ll define in the next few sections. Because radiance involves an angle measure in its definition, and the angle between two light beams refracted by Snell’s law is different before and after refraction, the ratio between outgoing and incoming radiance involves an extra factor of

$$\frac{\sin^2\theta_i}{\sin^2\theta_t}=\frac{n_2^2}{n_1^2}. \tag{26.16}$$

The derivation of this factor is given in the web materials for this chapter.

Although we’ve observed that light, after reflection, tends to be increasingly polarized, it’s common in graphics to treat light as **unpolarized**, that is, to assume that the polarization of incident light is, on average, zero. With that assumption, the Fresnel equations can be simplified to a single factor, called the Fresnel reflectance, which is

$$R_F=\frac{1}{2}(R_s+R_p). \tag{26.17}$$

The energy reflected is $R_F$ times the incident energy. And the energy transmitted is $(1-R_F)$ times the incident energy. This means that the reflected and transmitted radiance values can be computed as

$$L(P,\omega_r)=R_FL(P,-\omega_i) \quad\text{and} \tag{26.18}$$
$$L(P,\omega_t)=(1-R_F)\frac{n_2^2}{n_1^2}L(P,-\omega_i). \tag{26.19}$$

Note that $R_F$ here depends implicitly on $\theta_i$, $n_1$, and $n_2$, which, together with Snell’s law, lets us compute $\theta_t$.

# 26.6 Modeling Light as a Continuous Flow

Imagine standing at a crossroads, looking north. You count the cars that come to the crossroads from the north, and observe that 60 cars arrive in the course of an hour. You report that the arrival rate for cars is 60 per hour, and this lets you guess that in 10 minutes, about 10 cars will arrive; in 5 minutes 5 cars will arrive, etc. Of course, at an actual crossroads, cars arrive irregularly, so your “5 cars in 5 minutes” claim is probably not exactly correct. Nonetheless, if you counted cars for each hour over the course of the day, you could make a graph like the one shown in Figure 26.16, where we’ve connected the dots with straight lines, but could have used a smooth curve. Later you could say something like “the arrival rate at 9:30 was about 65 cars per hour.”

![](bbox=[0.741, 0.713, 0.92, 0.845])

*Figure 26.16: The number of cars arriving from the north at an intersection, at each hour.*

In making such a statement, you are treating the arrival rate as something that makes sense at a particular instant; you are treating this problem as if it were