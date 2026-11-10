We start by generating a striped pattern somewhat similar to the “stripes” example from earlier in this chapter—the new stripes differ from the previous ones, first because they are diagonal, and also because they are produced by a sine wave and therefore have blurry edges. We then use the noise map to perturb those lines, storing them as grayscale values. The changes to the fillDataArray() function are as follows:

```
~~~java
private void fillDataArray(byte data[])
{
  double veinFrequency = 2.0;
  double turbPower = 1.5;
  double maxZoom = 64;
  for (int i=0; i<noiseWidth; i++)
  {
    for (int j=0; j<noiseHeight; j++)
    {
      for (int k=0; k<noiseDepth; k++)
      {
        double xyzValue = (float) i / noiseWidth + (float) j / noiseHeight + (float)k / noiseDepth
            * turbPower * turbulence(j,k,maxZoom) / 256.0;
        double sineValue = Math.abs(Math.sin(xyzValue * 3.14159 * veinFrequency));
        Color c = new Color(sineValue, sineValue, sineValue);
        data[(noiseWidth*noiseHeight*4*i)+(noiseHeight*4*j)+4*k+0] = (byte) c.getRed();
        data[(noiseWidth*noiseHeight*4*i)+(noiseHeight*4*j)+4*k+1] = (byte) c.getGreen();
        data[(noiseWidth*noiseHeight*4*i)+(noiseHeight*4*j)+4*k+2] = (byte) c.getBlue();
        data[(noiseWidth*noiseHeight*4*i)+(noiseHeight*4*j)+4*k+3] = (byte) 255;
      } } }
~~~
```

The variable veinFrequency is used to adjust the number of stripes, maxZoom adjusts the zoom factor used when generating the turbulence, and turbPower adjusts the amount of perturbation in the stripes (setting it to zero leaves the stripes unperturbed). Since the same sine wave value is used for all three (RGB) color components, the final color stored in the image data array is grayscale: Figure 14.16

![](bbox=[0.12, 0.75, 0.88, 0.88])

**Figure 14.16**
Building 3D "marble" noise maps.