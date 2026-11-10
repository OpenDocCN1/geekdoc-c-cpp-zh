```
```cpp
for (int k=0; k<noiseDepth; k++) {
    data[(noiseWidth*noiseHeight*4) + j*(noiseHeight*4) + k*4 + 0] =
        (GLubyte) (smoothNoise(i/zoom, j/zoom, k/zoom) * 255);
    data[(noiseWidth*noiseHeight*4) + j*(noiseHeight*4) + k*4 + 1] =
        (GLubyte) (smoothNoise(i/zoom, j/zoom, k/zoom) * 255);
    data[(noiseWidth*noiseHeight*4) + j*(noiseHeight*4) + k*4 + 2] =
        (GLubyte) (smoothNoise(i/zoom, j/zoom, k/zoom) * 255);
    data[(noiseWidth*noiseHeight*4) + j*(noiseHeight*4) + k*4 + 3] = (GLubyte) 255;
} } } }

double smoothNoise(double zoom, double x1, double y1, double z1) {
    // fraction of x1, y1, and z1 (percentage from current block to next block, for this texel)
    double fracX = x1 - (int) x1;
    double fracY = y1 - (int) y1;
    double fracZ = z1 - (int) z1;

    // indices for neighboring values with wrapping at the ends
    double x2 = x1 - 1; if (x2<0) x2 = round(noiseWidth / zoom) - 1.0;
    double y2 = y1 - 1; if (y2<0) y2 = round(noiseHeight / zoom) - 1.0;
    double z2 = z1 - 1; if (z2<0) z2 = round(noiseDepth / zoom) - 1.0;

    // smooth the noise by interpolating the greyscale intensity along all three axes
    double value = 0.0;
    value += fracX        * fracY        * fracZ        * noise[(int)x1][(int)y1][(int)z1];
    value += (1-fracX)    * fracY        * fracZ        * noise[(int)x2][(int)y1][(int)z1];
    value += fracX        * (1-fracY)    * fracZ        * noise[(int)x1][(int)y2][(int)z1];
    value += (1-fracX)    * (1-fracY)    * fracZ        * noise[(int)x2][(int)y2][(int)z1];

    value += fracX        * fracY        * (1-fracZ)    * noise[(int)x1][(int)y1][(int)z2];
    value += (1-fracX)    * fracY        * (1-fracZ)    * noise[(int)x2][(int)y1][(int)z2];
    value += fracX        * (1-fracY)    * (1-fracZ)    * noise[(int)x1][(int)y2][(int)z2];
    value += (1-fracX)    * (1-fracY)    * (1-fracZ)    * noise[(int)x2][(int)y2][(int)z2];
    return value;
}
```
```

The smoothNoise() function computes a greyscale value for each texel in the smoothed version of a given noise map by computing a weighted average of the eight greyscale values surrounding the texel in the corresponding original “blocky” noise map. That is, it averages the color values at the eight vertices of the small “block” the texel is in. The weights for each of these “neighbor” colors are based on the texel’s distance to each of its neighbors, normalized to the range [0, 1]. Values at the ends wrap smoothly to facilitate tiling.

Next, smoothed noise maps of various zooming factors are *combined*. A new noise map is created in which each of its texels is formed by another weighted