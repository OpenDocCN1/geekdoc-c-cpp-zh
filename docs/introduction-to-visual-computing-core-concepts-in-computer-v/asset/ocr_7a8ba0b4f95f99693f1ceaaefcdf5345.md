often called the black offset. If this black offset is characterized by the XYZ coordinates (X_l, Y_l, Z_l), then the equation 10.9 becomes

```
(X, Y, Z) = O + i_r(R - O) + i_g(G - O) + i_b(B - O)  (10.12)
= (X_l, Y_l, Z_l)  (10.13)
+ i_r(X_r - X_l, Y_r - Y_l, Z_r - Z_l)  (10.14)
+ i_g(X_g - X_l, Y_g - Y_l, Z_g - Z_l)  (10.15)
+ i_r(X_b - X_l, Y_b - Y_l, Z_b - Z_l)  (10.16)
```

The above equation represented as a matrix becomes

```
\begin{pmatrix} X \\ Y \\ Z \end{pmatrix} = \begin{pmatrix} X_r - X_l & X_g - X_l & X_b - X_l & X_l \\ Y_r - Y_l & Y_g - Y_l & Y_b - Y_l & Y_l \\ Z_r - Z_l & Z_g - Z_l & Z_b - Z_l & Z_l \end{pmatrix} \begin{pmatrix} i_r \\ i_g \\ i_b \\ 1 \end{pmatrix}  (10.17)
```

# Fun Facts

![](bbox=[0.19, 0.57, 0.5, 0.75])

Interestingly, not only human perception of light, but all human perceptions follow a power law. This is called the Steven's power law based on the scientist who first made the observation. This law says that response R of any human perception to the input stimuli I follows the equation R = K I^γ. If γ > 1.0, perception is expansive. An example is electric shock. If γ < 1.0, perception is compressive. An example is our perception of brightness. γ is seldom 1.0. The expansive or compressive nature of our perception is shaped by evolution! The compressive nature of our perception to brightness saves our eyes from getting burned regularly by sunlight. The expansive nature of our perception to electric shock helps to put us on guard when the stimulus is not too large to cause damage.

However, note that the parameters of the matrix are not available to the user directly from the specification sheet of the devices. In general, they can be derived from other parameters that are specified. The first of these is a standardized 2D gamut. The 2D gamut of a device should usually conform to a predefined standard gamut, like sRGB, HD and NTSC (Figure 10.3). However, the 2D gamut