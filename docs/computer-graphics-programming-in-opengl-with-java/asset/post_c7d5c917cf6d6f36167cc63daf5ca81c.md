
can be achieved. Sampling 64 points per pixel, such as in Figure 8.21, is usually impractical.

A commonly used algorithm for implementing PCF is to sample four nearby texels per pixel, with the samples selected at specified offset distances from the texel which corresponds to the pixel. As we process each pixel, we alter the offsets used to determine which four texels are sampled. Altering the offsets in a staggered manner is sometimes called *dithering*, and aims to make the soft shadow boundary appear less “blocky” than it ordinarily would given the small number of sample points.

A common approach is to assume one of four different offset patterns—we can choose which pattern to use for a given pixel by computing the pixel’s `gl_FragCoord` mod 2. Recall that `gl_FragCoord` is of type vec2, containing the x and y coordinates of the pixel location; the result of the mod computation is then one of four values: (0,0), (0,1), (1,0), or (1,1). We use this result to select one of our four different offset patterns in texel space (i.e., in the shadow map).

The offset patterns are typically specified in the x and y directions with different combinations of −1.5, −0.5, +0.5, and +1.5 (these can also be scaled as desired). More specifically, the four usual offset patterns for each of the cases resulting from the `gl_FragCoord` mod 2 computation are

| case (0,0) | case (0,1) | case (1,0) | case (1,1) |
|---|---|---|---|
| *sample points:*<br>(sₓ − 1.5, sᵧ + 1.5)<br>(sₓ − 1.5, sᵧ − 0.5)<br>(sₓ + 0.5, sᵧ + 1.5)<br>(sₓ + 0.5, sᵧ − 0.5) | *sample points:*<br>(sₓ − 1.5, sᵧ + 0.5)<br>(sₓ − 1.5, sᵧ − 1.5)<br>(sₓ + 0.5, sᵧ + 0.5)<br>(sₓ + 0.5, sᵧ − 1.5) | *sample points:*<br>(sₓ − 0.5, sᵧ + 1.5)<br>(sₓ − 0.5, sᵧ − 0.5)<br>(sₓ + 1.5, sᵧ + 1.5)<br>(sₓ + 1.5, sᵧ − 0.5) | *sample points:*<br>(sₓ − 0.5, sᵧ + 0.5)<br>(sₓ − 0.5, sᵧ − 1.5)<br>(sₓ + 1.5, sᵧ + 0.5)<br>(sₓ + 1.5, sᵧ − 1.5) |

sₓ and sᵧ refer to the location (sₓ, sᵧ) in the shadow map corresponding to the pixel being rendered, identified as `shadow_coord` in the code examples throughout this chapter. These four offset patterns are illustrated in Figure 8.22, with each case shown in a different color. In each case, the texel corresponding to the pixel being rendered is at the origin of the graph for that case. Note that when shown together in Figure 8.23, the staggering/dithering of the offsets is apparent.

Let’s walk through the entire computation for a particular pixel. Assume the pixel being rendered is located at `gl_FragCoord = (48,13)`. We start by determining the four shadow map sample points for the pixel. To do that, we would compute `vec2(48,13) mod 2`, which equals (0,1). From that we would choose the offsets shown for case (0,1), shown in green in Figure 8.22, and the specific points to be sampled in the shadow map (assuming that no scaling of the offsets has been specified) would be

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_235_0.png)

**Figure 8.22** Dithered four-pixel PCF sampling cases.

- `(shadow_coord.x−1.5, shadow_coord.y+0.5)`
- `(shadow_coord.x−1.5, shadow_coord.y−1.5)`
- `(shadow_coord.x+0.5, shadow_coord.y+0.5)`
- `(shadow_coord.x+0.5, shadow_coord.y−1.5)`

(Recall that `shadow_coord` is the location of the texel in the shadow map corresponding to the pixel being rendered—shown as a white circle in Figures 8.22 and 8.23.)

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_235_1.png)

**Figure 8.23** Dithered four-pixel PCF sampling (four cases shown together).

We next call `textureProj()` on each of these four points, which in each case returns either 0.0 or 1.0 depending on whether or not that sampled point is in shadow. We sum the four results and divide by 4.0 to determine the percentage of sampled points which are in shadow. This percentage is then used as a multiplier to determine the amount of diffuse and specular lighting to be applied when rendering the current pixel.

Despite the small sampling size—only 4 samples per pixel—this dithered approach can often produce surprisingly good soft shadows. Figure 8.24 was generated using 4-point dithered PCF. While not quite as good as the 64-point sampled version shown previously in Figure 8.21, it renders considerably faster.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_235_2.png)

**Figure 8.24** Soft shadow rendering—four samples per pixel, dithered.

## 8.7.3 A Soft Shadow/PCF Program

As mentioned earlier, the soft shadow computation can be done entirely in the fragment shader. Program 8.2 shows the fragment shader that replaces the one in Figure 8.7. The PCF additions are highlighted.

### Program 8.2 Percentage Closer Filtering (PCF)

Fragment Shader

```glsl
#version 430
// all variable declarations are unchanged
...

// Returns the shadow depth value for a texel at distance (x,y) from shadow_coord. Recall that
// shadow_coord is the location in the shadow map corresponding to the current pixel being rendered.
float lookup(float ox, float oy)
{
    float t = textureProj(shadowTex,
        shadow_coord + vec4(ox * 0.001 * shadow_coord.w, oy * 0.001 * shadow_coord.w,
            -0.01, 0.0)); // the third parameter (-0.01) is an offset to counteract shadow acne
    return t;
}

void main(void)
{
    float shadowFactor = 0.0;
    vec3 L = normalize(vLightDir);
    vec3 N = normalize(vNormal);
    vec3 V = normalize(-v_matrix[3].xyz - varyingVertPos);
    vec3 H = normalize(vHalfVec);

    // ----- this section produces a 4-sample dithered soft shadow
    float swidth = 2.5;       // tunable amount of shadow spread
    // produces one of 4 sample patterns depending on gl_FragCoord mod 2
    vec2 offset = mod(floor(gl_FragCoord.xy), 2.0) * swidth;
    shadowFactor += lookup(-1.5*swidth + offset.x, 1.5*swidth - offset.y);
    shadowFactor += lookup(-1.5*swidth + offset.x, -0.5*swidth - offset.y);
    shadowFactor += lookup(0.5*swidth + offset.x, 1.5*swidth - offset.y);
    shadowFactor += lookup(0.5*swidth + offset.x, -0.5*swidth - offset.y);
    shadowFactor = shadowFactor / 4.0;  // shadowFactor is an average of the four sampled points

    // ----- this section, if un-commented, produces a 64-sample hi resolution soft shadow
    // float swidth = 2.5;       // tunable amount of shadow spread
    // float endp = swidth*3.0 + swidth/2.0;
    // for (float m=-endp; m<=endp; m=m+swidth)
    // {
    //     for (float n=-endp; n<=endp; n=n+swidth)
    //     {
    //         shadowFactor += lookup(m,n);
    //     }
    // }
    // shadowFactor = shadowFactor / 64.0;

    vec4 shadowColor = globalAmbient * material.ambient + light.ambient * material.ambient;

    vec4 lightedColor = light.diffuse * material.diffuse * max(dot(L,N),0.0)
                      + light.specular * material.specular
                      * pow(max(dot(H,N),0.0),material.shininess*3.0);

    fragColor = vec4((shadowColor.xyz + shadowFactor*(lightedColor.xyz)),1.0);
}
```

The fragment shader shown in Program 8.2 contains code for both the 4-sample and 64-sample PCF soft shadows. First, a function `lookup()` is defined to make the sampling process more convenient. It makes a call to the GLSL function `textureProj()` that does a lookup in the shadow texture, but offset by a specified amount (ox,oy). The offset is multiplied by 1/windowSize, which here we have simply hardcoded to .001 assuming a window size of 1000×1000 pixels.²

The 4-sample dithered computation appears highlighted in `main()` and follows the algorithm described in the previous section. A scale factor swidth has been added that can be used to adjust the size of the “soft” region at the edge of the shadows.

The 64-sample code follows, and is commented out. It can be used instead of the 4-sample computation, by uncommenting it and instead commenting out the 4-sample code. The swidth scale factor in the 64-sample code is used as a step size in the nested loop that samples points at various distances from the

² We have also multiplied the offset by the w component of the shadow coordinate, because OpenGL automatically divides the input coordinate by w during texture lookup. This operation, called *perspective divide*, is one which we have ignored up to this point. It must be accounted for here. For more information on *perspective divide*, see [LO12].
