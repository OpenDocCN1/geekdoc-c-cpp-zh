```
for (int i=0; i<noiseWidth; i++) {
    for (int j=0; j<noiseHeight; j++) {
        for (int k=0; k<noiseDepth; k++) {
            double xyzValue = (float)i / noiseWidth + (float)j / noiseHeight + (float)k / noiseDepth
                + turbPower * turbulence(i,j,k,maxZoom) / 256.0;
            double sineValue = abs(sin(xyzValue * 3.14159 * veinFrequency));

            float redPortion = 255.0f * (float)sineValue;
            float greenPortion = 255.0f * (float)sineValue;
            float bluePortion = 255.0f * (float)sineValue;

            data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+0] = (GLubyte) redPortion;
            data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+1] = (GLubyte) greenPortion;
            data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+2] = (GLubyte) bluePortion;
            data[i*(noiseWidth*noiseHeight*4)+j*(noiseHeight*4)+k*4+3] = (GLubyte) 255;
        }
    }
}
```

The variable veinFrequency is used to adjust the number of stripes, turbSize adjusts the zoom factor used when generating the turbulence, and turbPower adjusts the amount of perturbation in the stripes (setting it to zero leaves the stripes unperturbed). Since the same sine wave value is used for all three (RGB) color components, the final color stored in the image data array is grayscale. Figure 14.16 shows the resulting texture map for various values of turbPower (0.0, 0.5, 1.0, and 1.5, left to right).

We can further control the definition and thickness of the marble veins by modifying the turbulence() function so that it uses a logistic function. A logistic (or “sigmoid”) function has an S-shaped curve with asymptotes on both ends. Common examples are hyperbolic tangent and f(x) = 1/(1+e⁻ˣ). They are also sometimes called “squashing” functions. Many noise applications utilize a logistic function to push the values in the noise map more towards 0.0 or 255.0, rather than

![](bbox=[0.147, 0.738, 0.852, 0.879])

**Figure 14.16**  
Building 3D “marble” noise maps.