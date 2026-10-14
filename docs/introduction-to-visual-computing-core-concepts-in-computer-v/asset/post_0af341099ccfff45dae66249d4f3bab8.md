
## Exercises

1. Consider a 2D square on the XY plane with side 2 units, the center at the origin and four sides parallel or perpendicular to the coordinate axes.

+   (a) Draw the picture of the transformed square after performing the following sequence operations: rotation of 45 degrees counter clockwise about Z-axis, translation by (√2,0,0), and again a rotation of 45 degrees counter clockwise about Z-axis. Can you reduce the transformations thus giving the new sequence of transformation to achieve the same result?

+   (b) Draw the picture of the transformed square after performing the following sequence of operations: translation by (2,2,0), scaling by (3,2,1).

+   (c) Draw the picture of the square if these two operations in the previous question were swapped.

+   (d) We would like to achieve the result of the transformations of the previous questions where scaling is followed by translation by applying a translation followed by scaling. How would the parameters of the translation and the scaling change?

2. A viewer is defined by the following. (a) Eye position: (0,0,0), (b) View up vector: (0,2,0), (c) Equation of the image plane: x + y + z = 6. Find the view transformation matrix generated for this view-setup. Let the left, right, top and bottom planes be at -2, +2, 4, and 8 respectively. Let the far plane be at 10. Find the perspective projection matrix given by L. Find what would be projected coordinates of a point P = (10,4,6) for this viewer.

3. The model transformation for a scene is a rotation R about the Y axis in the counter clockwise direction by 90 degrees, followed by a translation T in the positive X direction by 20 units. What is the resulting transformation?

4. Consider a default view with the near plane (or image plane) at a distance 5. The gaze direction is at (2,1) and the size of the window in X and Y direction in which it is centered are 10 and 6 respectively.

+   (a) Provide the r, l, t, b for the view frustum?

+   (b) Provide the transformation that would make the gaze direction coincident with the normal to the image plane?

+   (c) Following this, find the transformation to normalize X and Y coordinates between −1 to +1.

5. Provide the window coordinate transformation for a window whose center is located at (200, 400) and whose width and height are given by 800 and 600 respectively?

6. We say that interpolation of Z in screen space is mathematically wrong and we should interpolate the reciprocal of Z to correct for the effect. Yet, we interpolate colors using the same screen space interpolation. Is this mathematically correct? Justify your answer.

## Realism and Performance

In the last chapter, we discussed the geometric fundamentals of the interactive graphics pipeline. However, a scene rendered using this basic pipeline with no lighting effects (e.g. specular highlights or shadows) or finer details or some patterns or bumps on objects would not look realistic. In this chapter, we will study a number of techniques that will allow us to render more realism in the scene. However, these do not come for free, rather with a risk of degrading performance (e.g. frame rate). Therefore, we will also discuss some techniques to enhance realism without compromising performance.

### 14.1 Illumination

Computing illumination of a scene is an extremely complex problem. The total amount of illumination at any surface point is due to both *direct* and *indirect* illumination. Direct illumination accounts for the light coming directly from a light source and reaching a surface point on the object. In addition, light reflected off, transmitted through or refracted by other surfaces can also reach the same surface point after multiple bounces and is called the indirect illumination. Thus, in order to compute that total amount of illumination at any surface point on an object we need to compute all the indirect illumination resulting from multiple bounces across multiple surfaces in addition to the direct illumination from the light source, as summarized in Equation 9.23 of Chapter 9. Such compute-intensive complex light models can be extremely time-consuming and therefore not suitable for interactive graphics. Therefore, much simpler illumination models are used to meet the interactive rates performance criterion.

The first simplification comes from assuming point light sources where we will start our discussion. Second, only the direct illumination (i.e. the light that comes at a point on the object directly from the point light source) is modeled while all the indirect illumination (i.e. light that reaches a point after bouncing multiple times from multiple objects) is combined under a single term called *ambient illumination*.

Let us consider a single light source illuminating a surface point *P* with normal N from the direction L and the eye looking at this point from the direction V as in Figure 14.1. Let R be the vector formed by reflecting L about the normal N. Note the similarity between the figures 14.1 and 9.1. Let the intensity of the light be I. The ambient illumination I_a is modeled very simplistically as

```
I_a = c_a I
```

where c_a is called the coefficient for ambient illumination.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_334_0.png)

Figure 14.1. This illustrates the parameters for the simple ambient, diffused and specular illumination models at P.

The direct illumination is modeled in two parts – the view-independent component (that remains constant with change in view point and direction) called the diffused component and the view-dependent component (that changes with change in view point and direction) called the specular component. Different illumination models differ in the way they compute the specular component. We will discuss the most commonly used Phong Illumination model named after Bui Tong Phong. But more complicated models (e.g. Cook Torrance model) can also be employed for this purpose at the cost of performance.

The view-independent diffused illumination I_d is given by

```
I_d = c_d I (N · L) = c_d I cosθ
```

where c_d is called the coefficient of diffused reflection. Note the similarity of this equation with Equation 9.22 in Chapter 9. c_d in Equation 14.2 is equivalent to ρ in Equation 9.22. However, since the amount of light reflected in the direction of the viewer is independent of his location, c_d does not have any dependency on V.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_334_1.png)

Figure 14.2. This figure shows the function cos^s(φ) for different values of s.

A specular component of the Phong illumination model is given by

```
I_s = c_s I cos(R·V)^s = c_s I (cos(φ))^s
```

where c_s is the coefficient for specular reflection and s is a parameter that controls the size of the view-dependent specular highlight. Figure 14.2 shows how the cosine fall off becomes steeper as s increases to achieve this effect. Since R depends on the incident direction L with respect to the normal vector N, and

![](img/66c45bbed85bb7ba7f7b05dff49b5060_335_0.png)

**Figure 14.3.** This illustrates effect of the parameters $c_d$ and $c_s$ of the simple illumination model. (a) and (b) show diffused illumination where $c_d$ for latter is smaller than that of the former. (c), (d) and (e) show the specular illumination where (c) and (d) has smaller $s$ than (e) while (d) has smaller $c_s$ than (c) and (e).

the measurement of light is done in the outgoing direction $V$, the term $c_s(R \cdot V)$ in Equation 14.3 is equivalent to $\rho(k_i, k_o)$ in Equation 9.22.

Figure 14.3 shows the effect of these parameters on the illumination. Assuming that light direction, intensity and distance from the surface point remains the same (given by $L$), we consider a sampling of the light vectors, indicating the amount of light seen in that direction, in red. (a) and (b) shows diffused reflection where equal amount of light is reflected in all directions illustrated by the equal length of the red vectors. Therefore, the amount of light received by the viewer $V$ is the same irrespective of the angle between $R$ and $V$. However, (b) has a smaller $c_d$ illustrated by the fact that the vectors in (b) are shorter than those in (a). (c), (d) and (e) all show specular reflection where the length of the reflected vectors, indicating the amount of light seen in that direction, change based on how much the vector $V$ deviate from the reflected vector $R$. If $V$ is aligned with $R$, the light reaching $V$ would be the maximum and would diminish as the angle between $R$ and $V$ reduce. Hence, specular illumination is view-dependent. (d) has smaller $c_s$ than (c) while the directions in which they are reflected remain the same. However, (e) has a sharper view dependency shown by a sharper lobe in the outgoing light direction. Therefore, $s$ controls the sharpness of the view-dependency as shown in Figure 14.2.

Figure 14.4 shows the effect of different parameters of the aforementioned Phong illumination model. Note that with the increase in $c_a$, the entire object looks brighter and shows no dependence on the direction of light, as is expected. On the contrary, when $c_d$ is increased the shadow effect becomes more prominent since the directionality of the lighting plays a role. You can also see the effect of $c_s$ and $s$ on specular lighting. While $c_s$ changes the amount of light reflected without changing the size of the highlight, changing $s$ changes the size of the highlight.

Finally, Figure 14.5 shows the combined effect of the ambient, diffused and specular illumination under a point light source. Although the Phong model is
