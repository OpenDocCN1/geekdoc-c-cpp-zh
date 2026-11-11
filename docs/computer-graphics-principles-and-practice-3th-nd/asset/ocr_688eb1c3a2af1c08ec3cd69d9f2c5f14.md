is not an emitter, but there is direct light from $R$ to $P$, shown in cyan. Notice that this division of light arriving at $P$ from $Q$ into different parts is a mathematical convenience. There's no way, when a photon arrives at $P$ from $Q$, to tell whether it was directly emitted or was scattered. But dividing the arriving light in this way allows us to structure our program to get better results.

The figure also shows the results of scattering these at $P$, which we'll call $L^{ds}$ and $L^{is}$. The scattered radiance $L^s$ is just $L^{ds}+L^{is}$. Thus,

$$L^{i,s}(P,\omega)=\int L^i(Q,\omega_i) f_s(Q,\omega,\omega_i)|\omega_i\cdot \mathbf{n}_Q|\,d\omega_i, \qquad (31.92)$$
$$L^{d,s}(P,\omega)=\int L^d(Q,\omega_i) f_s(Q,\omega,\omega_i)|\omega_i\cdot \mathbf{n}_Q|\,d\omega_i, \qquad (31.93)$$

where $Q=\operatorname{raycast}(P,\omega)$.

With these definitions, we restructure the code slightly (see Listing 31.5).

# Listing 31.5: Kajiya-style path tracer, part 1.

```
    define estimateL(C, ω):
        P = raycast(C, -ω)
        resultSum = Le(P, ω) + estimateLr(P, ω)
        return resultSum

    define estimateLr(P, ω):
        return estimateLds(P, ω) + estimateLis(P, ω)

    define estimateLis(P, ω): // single sample estimate
        u = uniform(0, 1)
        ρ = scatterFraction(P)
        if (u < ρ):
            ωi = randsphere()
            Q = raycast(P, ωi)
            integrand = Le(Q, -ωi) * f_s(P, ω, ωi) |ωi · n|
            density = 1/(4π)

            return integrand / (ρ * density)
        return 0

    define estimateLds(...
```

Notice that in estimating the scattered indirect light, we didn't scatter all the radiance arriving at $P$ from $Q$, but only $L^i$. The $L^e$ portion of the radiance is the direct light, which we're deliberately not including.

To estimate $L^{ds}$ (the scattering of the direct light), we are trying to evaluate the integral

$$L^{d,s}(P,\omega)=\int L^e(Q,-\omega_i) f_s(P,\omega,\omega_i)|\omega_i\cdot \mathbf{n}_P|\,d\omega_i, \qquad (31.94)$$

where $Q$ denotes the result of a ray cast from $P$ in direction $\omega_i$.

We're going to shift from a spherical integral to a surface integral (which involves the usual change of variable), and integrate over all light sources. (You should now think of $Q$ as being a point on the light source in Figure 31.24.) To keep things simple, we'll assume that we have only area light sources (no point lights!), and that there are $K$ of them, with areas $A_1,\ldots,A_K$, and total area $A=A_1+A_2+\cdots+A_K$.