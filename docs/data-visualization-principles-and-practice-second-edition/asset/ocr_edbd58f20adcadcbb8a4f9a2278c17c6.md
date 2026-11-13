# 10.2.7 Volumetric Shading

As mentioned previously, shading is an important additional cue that can significantly increase the quality of volume renderings. In the case of isosurfaces (see Section 10.2.5), for example, shading is an indispensable element. Shading can be easily combined with the volume illumination integral given by Equation (10.11). Instead of directly using the colors $c(t) = f(s(t))$ delivered by the application of the color transfer function $f$ on the scalar values $s(t)$ along the ray in the volume integral, we can use instead an illumination function

$I(t) = c_{amb} + c_{diff}(t) \max(-\mathbf{L} \cdot \mathbf{n}(t), 0) + c_{spec}(t) \max(\mathbf{r} \cdot \mathbf{v}, 0)^\alpha$. (10.12)

This is nothing more than the application of the Phong lighting model (see Equation (2.11)) to an imaginary surface located at the current point $t$ along the ray, having the normal $\mathbf{n}$. Here, $c_{amb}$ is the ambient lighting factor, which is constant for the entire volume. $c_{diff}(t)$ and $c_{spec}(t)$ are the diffuse and specular lighting factors, respectively, which typically are functions of position $t$. In a simple approximation, we can set $c_{diff}(t) = c_{spec}(t) = c(t)$. The vectors $\mathbf{L}$, $\mathbf{r}$, and $\mathbf{v}$ have the same meaning as in the original Phong lighting model (Equation (2.11)).

To apply the preceding lighting model, we need to estimate a surface normal $\mathbf{n}(t)$. For most locations in a volume dataset, we cannot actually speak about the existence of a physical surface. However, we can define such a surface as being the isosurface for the isovalue $s(t)$, which exists for every point. As explained in Section 5.3, the gradient of a function is normal to the function’s contours. Hence, we can estimate the normal $\mathbf{n}(t)$ by computing the gradient vector of the scalar signal $s$

$\nabla s(t) = \left( \frac{\partial s(t)}{\partial x}, \frac{\partial s(t)}{\partial y}, \frac{\partial s(t)}{\partial z} \right)$ (10.13)

and normalizing the result to unit length. The partial derivatives of $s$ with respect to the coordinate axes $x, y, z$ can be computed as described in Section 3.7 by interpolating the discrete partial derivatives evaluated at the voxel corners.

Although this solution is possible, it can deliver noisy results in practice, as the gradient is quite sensitive to small-scale noise in the sampled dataset. This translates into small-scale wavy artifacts in the final shading, which are quite disturbing, especially if specular lighting is used. To enhance the robustness of the gradient estimation, we can apply several of the filtering techniques discussed for image processing in Chapter 9, such as the Sobel or Prewitt operators, or prefilter the scalar dataset prior to the gradient estimation.

Figure 10.11 illustrates the effects of volumetric lighting on a dataset rendered with a composite ray function. The transfer functions emphasize the hard