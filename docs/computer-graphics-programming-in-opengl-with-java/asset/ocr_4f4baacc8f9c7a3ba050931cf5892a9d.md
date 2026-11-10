The noise map is built using the code from Section 14.5, with a slight modification to the turbulence() function. Specifically, we add a sine wave that runs diagonally across the XZ plane:

```
```java
private double turbulence(double x, double y, double z, double maxZoom)
{  double sum = 0.0, zoom = maxZoom;
   sum = Math.sin(1/512.0*PI*(x+z) + 1) * 8.0;
   while(zoom >= 0.9)
   {  sum = sum + smooth(zoom, x/zoom, y/zoom, z/zoom) * zoom;
      zoom = zoom / 2.0;
   }
   sum = 128.0 * sum/maxZoom;
   return sum;
}
```
```

The diagonal sine wave is accomplished via sin(x+z), with additional factors for scaling (1/512 assuming that the size of the noise map is 256 along the X and Z dimensions), ensuring that the range of values for x+y span a multiple of PI so that the sine wave wraps smoothly at edge boundaries, adding 1 to convert the sine wave from -1..+1 to 0..2, and then scaling the height to the desired amount (in this case, by a factor of 8). Note that since we have been making heavy use of tiling, it is especially important in this application to use a noise map dimension that is a power of 2, so that the noise also wraps smoothly at edge boundaries.

We then pass the noise map to the fragment shader, where we use it to alter the normals by a very small offset. The additions to the code are shown in Program 15.4. The resulting output is shown in Figure 15.6.

# Program 15.4 Adding Surface Waves

*Java/JOGL Application*

```
```java
...
private int noiseTexture;
private int noiseHeight = 256;
private int noiseWidth = 256;
private int noiseDepth = 256;
private double[][][] noise = new double[noiseWidth][noiseHeight][noiseDepth];
...
// buildNoiseTexture(), fillDataArray(), smoothNoise() same as in Chapter 14
// turbulence() function as described above
...
```
```