# Figure 6.12 Diagram of Phong reflection calculations (vectors not to scale)

In the Phong reflection model, you calculate the light applied to a surface as follows:

```
Ambient = k_a
Diffuse = k_d(\hat{n} \cdot \hat{l})
Specular = k_s(\hat{r} \cdot \hat{v})^\alpha
Phong = Ambient + \sum_{\forall lights} \begin{cases} Specular + Diffuse & \text{if } \hat{n} \cdot \hat{l} > 0 \\ 0 & \text{otherwise} \end{cases}
```

```
Ambient = k_a
Diffuse = k_d(\hat{n} \cdot \hat{l})
Specular = k_s(\hat{r} \cdot \hat{v})^\alpha
Phong = Ambient
+ \sum_{\forall light} \begin{cases} Specular + Diffuse & \text{if } \hat{n} \cdot \hat{l} > 0 \\ 0 & \text{otherwise} \end{cases}
```

Note that the diffuse and specular component computes for all lights in the scene, but there's only one ambient component. The \(\hat{n} \cdot \hat{l}\) test ensures that the light affects only surfaces facing the light.

In any event, the Phong equation as described here yields a color for all lights in the scene. The final color of the surface is the light color multiplied by the color of the surface. Because both the light and surface color are RGB values, you use component-wise multiplication.

A more complex implementation separates the surface