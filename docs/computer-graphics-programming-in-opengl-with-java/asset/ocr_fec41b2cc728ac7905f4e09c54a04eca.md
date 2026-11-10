![](bbox=[0.145, 0.08, 0.86, 0.18])

**Figure 8.22**
Dithered four-pixel PCF sampling cases.

For case (0,1), shown in green in Figure 8.22, and the specific points to be sampled in the shadow map (assuming that no scaling of the offsets has been specified) would be

+   - `(shadow_coord.x−1.5, shadow_coord.y+0.5)`
+   - `(shadow_coord.x−1.5, shadow_coord.y−1.5)`
+   - `(shadow_coord.x+0.5, shadow_coord.y+0.5)`
+   - `(shadow_coord.x+0.5, shadow_coord.y−1.5)`

(Recall that `shadow_coord` is the location of the texel in the shadow map corresponding to the pixel being rendered—shown as a white circle in Figures 8.22 and 8.23.)

![](bbox=[0.6, 0.335, 0.88, 0.505])

**Figure 8.23**
Dithered four-pixel PCF sampling (four cases shown together).

We next call `textureProj()` on each of these four points, which in each case returns either 0.0 or 1.0 depending on whether or not that sampled point is in shadow. We sum the four results and divide by 4.0 to determine the percentage of sampled points which are in shadow. This percentage is then used as a multiplier to determine the amount of diffuse and specular lighting to be applied when rendering the current pixel.

Despite the small sampling size—only 4 samples per pixel—this dithered approach can often produce surprisingly good soft shadows. Figure 8.24 was generated using 4-point dithered PCF. While not

![](bbox=[0.55, 0.7, 0.88, 0.9])

**Figure 8.24**
Soft shadow rendering—four samples per pixel, dithered.