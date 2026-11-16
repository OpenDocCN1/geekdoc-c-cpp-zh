
```
// Calculate coordinates for second pair of samples
coord = velo.xyxy * vec4(3.5, 3.5, -3.5, -3.5) +
sample.xyz = texRECT(colorTexture, coord.xy).xyz
depth = texRECT(velocityTexture, coord.xy).z;
if (depth >= minDepth) color += sample;

sample.xyz = texRECT(colorTexture, coord.zw).xyz
depth = texRECT(velocityTexture, coord.zw).z;
if (depth >= minDepth) color += sample;

// Calculate coordinates for third pair of samples
coord = velo.xyxy * vec4(5.25, 5.25, -5.25, -5.25)
gl_FragCoord.xyxy;
sample.xyz = texRECT(colorTexture, coord.xy).xyz
depth = texRECT(velocityTexture, coord.xy).z;
if (depth >= minDepth) color += sample;

sample.xyz = texRECT(colorTexture, coord.zw).xyz
depth = texRECT(velocityTexture, coord.zw).z;
if (depth >= minDepth) color += sample;

// Calculate coordinates for fourth pair of samples
coord = velo.xyxy * vec4(7.0, 7.0, -7.0, -7.0) +
sample.xyz = texRECT(colorTexture, coord.xy).xyz
depth = texRECT(velocityTexture, coord.xy).z;
if (depth >= minDepth) color += sample;

sample.xyz = texRECT(colorTexture, coord.zw).xyz
depth = texRECT(velocityTexture, coord.zw).z;
if (depth >= minDepth) color += sample;

// Total weight of used color samples is in the
// Divide by it to get the final averaged color.
gl_FragColor.xyz = color.xyz / color.w;
}
```

The velocity-depth-gradient buffer is read at the location of the center pixel, and the minimum depth required for all color samples is calculated as

(17.9) \( z_{\min} = z - r_{\max} \max\{g, 0.001\} \),

where z is the depth stored in the blue channel of the buffer, g is the depth gradient given by Equation (17.8) stored in the alpha channel of the buffer, and \( r_{\max} \) is the largest distance between the center pixel and a sample location. This is a little different from Equation (17.1) because we use the maximum sample distance \( r_{\max} \) to compute a single minimum depth \( z_{\min} \) that is used for all sample values. We clamp the minimum value of the gradient to 0.001 so that precision errors don't prevent the motion blur effect from working on surfaces that are nearly perpendicular to the view direction.

The value of \( r_{\max} \) is 7.0 in the fragment shader shown in Listing 17.3, and color samples are taken at offsets given by the velocity vector multiplied by the values 1.75, 3.5, 5.25, and 7.0. At each sample location, the velocity buffer is read, but only to fetch the depth at that sample location and compare it to \( z_{\min} \). (Velocity and gradient information is only used at the center pixel.) For any sample satisfying \( z \ge z_{\min} \), we add the color sample to the final color and add one to the number of valid samples (in the w component of the color). After all samples have been taken, we divide the final color by the number of valid samples that have been accumulated and output the result.

### 17.4 Grid Optimization

The fragment shader presented in Listing 17.3 produces very precise results, but it can be unnecessarily expensive for large parts of the scene. When it is known that a region of the screen contains pixels that are all moving at similar speeds relative to the camera, a simpler shader that does not consider depth can be used in order to increase overall performance. The use of the full implementation can be limited to those areas of the screen in which slow-moving foreground objects are expected to appear.

In Figure 17.4, we have divided the screen into a 16×12 grid of rectangular cells. Before rendering the post-processing shader, we determine whether any foreground objects might be slow moving relative to the background and mark cells covered by those objects as requiring the full-blown shader. This would typically be done when objects are being rendered into the velocity buffer near the beginning of the frame. In the post-processing phase, we apply the simpler, faster shader to cells that have not been marked.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_395_0.png)

Figure 17.4: (See also Color Plates.) In this image, the viewport is partitioned into a grid of 16×12 cells. The depth and gradient information is only used in the highlighted cells surrounding the character since that is where foreground objects are likely to be moving slowly relative to the background. (Image courtesy of Terathon Software LLC.)

### References

- [1] Gilberto Rosado. "Motion Blur as a Post-Processing Effect". GPU Gems 3, Addison-Wesley, 2008.
- [2] Ben Padget. "Efficient Real-Time Motion Blur for Multiple Rigid Objects". ShaderX7. Charles River Media, 2009.
- [3] C4 Engine. http://www.terathon.com/c4engine/

## Chapter 18: Fast Screen-Space Ambient Occlusion and Indirect Lighting

László Szirmay-Kalos, Balázs Tóth, and Tamás Umenhoffer

Budapest University of Technology and Economics

### 18.1 Introduction

A physically correct approach to rendering would be the solution of the rendering equation, but it is too expensive computationally when dynamic scenes are processed in real time. Thus in practice, we prefer approximations that can be efficiently evaluated. A usual simplification is the local illumination model, which computes only the direct contribution of the light sources and adds a constant ambient term for the missing indirect illumination. However, constant ambient lighting ignores the geometry of the scene, which results in plain and unrealistic images. We need better compromises between the rendering equation and the classical ambient model.

Local approaches examine only a neighborhood of the shaded point during illumination calculation. The obscurances method [10, 2], which is also called the ambient occlusion [1, 6] computes just how "open" the scene is in the neighborhood of a point, and scales the ambient light accordingly. To compute occlusions in real time, the method called screen-space ambient occlusion [5] examines the height field defined by the current content of the depth buffer instead of the real scene's geometry. Thus, when a point is shaded, the required geometric information about the rest of the scene is fetched from a depth texture. The classical ambient occlusion approach assumes that no illumination comes from nearby occluders. However, using the albedo or the color of these points, local indirect lighting can also be approximated [10, 8].

In this article, we present a simplified illumination model that is derived from the rendering equation. The model consists of two parts, the ambient occlusion part describing the influence of the distant part of the scene, and the indirect illumination part, which is responsible for local interactions. Both parts are directional integrals, which would need many discrete samples for an accurate estimation. In order for the efficient evaluation, we transform these integrals. The ambient occlusion integral is first transformed to a volumetric integral, which is first evaluated along the depth coordinate analytically, then the remaining integral over the disk perpendicular to the viewing direction is obtained numerically. The indirect lighting integral is expressed from the stable ambient occlusion estimate. Thus, our method is more general than [10] since it also takes into account the one-bounce of the direct lighting, and it is more robust than [8] since it does not include infinite variation form factors in the approximation.

The proposed method falls into the category of screen-space techniques since we assume that the depth buffer is the sampled representation of the scene geometry and the color buffer stores the radiance values of the represented surfaces. However, we work in camera space rather than in screen space to obtain correct distance and angle values.

The input of our rendering method includes the textures of camera-space depth values, normal vectors of the visible points, and the color buffer storing the radiances due to direct lighting. From these input textures, a deferred shading algorithm computes the radiances of the visible points, taking into account ambient occlusion and local indirect illumination.
