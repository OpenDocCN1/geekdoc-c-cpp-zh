properties. When the coefficients of the expansion are summed to determine field values, the function appears as a pulse train. The pulses have the domain of half of the highest resolution wavelet. Furthermore, these pulses overlap the constant valued sections of the highest resolution wavelets. A linear combination of the wavelet/ scaling functions has as many degrees of freedom as the number of coefficients used. There are $2^{r_{max}+1}$ functions used per level, and any finite real value can be represented at the center of each half of the $r_{max}$ level wavelets.

The effect of the variable grid when it is used to represent electromagnetic fields can be easily seen. If the field value can be approximated as constant across the half-domain of the highest resolution wavelet, there is no need for increasing resolution. If the field has more rapid variation, each increase in resolution doubles the effective resolution of the cell. High-resolution cells can be used to represent rapid field variation (such as impressed currents and discontinuity effects) while low-resolution cells can be used elsewhere.

# The equations

```
$$
\frac{dE_x}{dt} = \frac{1}{\epsilon} \frac{dH_z}{dy}
$$ (10.68)
```

```
$$
\frac{dE_y}{dt} = -\frac{1}{\epsilon} \frac{dH_z}{dx}
$$ (10.69)
```