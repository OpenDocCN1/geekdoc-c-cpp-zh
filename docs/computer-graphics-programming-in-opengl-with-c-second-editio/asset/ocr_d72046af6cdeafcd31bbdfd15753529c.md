We start by building a procedural “rings” 3D texture map, similar to the “checkerboard” from earlier in this chapter. We then use a noise map to perturb those rings, inserting dark and light brown colors into the ring texture map. By adjusting the number of rings, and the degree to which we perturb the rings, we can simulate wood with various types of grain. Shades of brown can be made by combining similar amounts of red and green, with less blue. We then apply Phong shading with a low level of “shininess.”

We can generate rings encircling the Z-axis in our 3D texture map by modifying the fillDataArray() function, using trigonometry to specify values for X and Y that are equidistant from the Z axis. We use a sine wave to repeat this process cyclically, raising and lowering the red and green components equally based on this sine wave to produce the varying shades of brown. The variable sineValue holds the exact shade, which can be adjusted by slightly offsetting one or the other (in this case increasing the red by 80, and the green by 30). We can create more (or fewer) rings by adjusting the value of xyPeriod. The resulting texture is shown in Figure 14.18.

```
```cpp
void fillDataArray(GLubyte data[ ]) {
    double xyPeriod = 40.0;
    for (int i=0; i<noiseWidth; i++) {
        for (int j=0; j<noiseHeight; j++) {
            for (int k=0; k<noiseDepth; k++) {
                double xValue = (i - (double)noiseWidth/2.0) / (double)noiseWidth;
                double yValue = (j - (double)noiseHeight/2.0) / (double)noiseHeight;
                double distanceFromZ = sqrt(xValue * xValue + yValue * yValue);
                double sineValue = 128.0 * abs(sin(2.0 * xyPeriod * distanceFromZ * 3.14159));
                float redPortion = (float)(80 + (int)sineValue);
                float greenPortion = (float)(30 + (int)sineValue);
                float bluePortion = 0.0f;
                data[(noiseWidth*noiseHeight*4)+(noiseHeight*4*k)+4*j+0] = (GLubyte) redPortion;
                data[(noiseWidth*noiseHeight*4)+(noiseHeight*4*k)+4*j+1] = (GLubyte) greenPortion;
                data[(noiseWidth*noiseHeight*4)+(noiseHeight*4*k)+4*j+2] = (GLubyte) bluePortion;
                data[(noiseWidth*noiseHeight*4)+(noiseHeight*4*k)+4*j+3] = (GLubyte) 255;
            } } } }
```
```

The wood rings in Figure 14.18 are a good start, but they don’t look very realistic—they are too perfect. To improve this, we use the noise map (more