Next, the fillDataArray() function from Program 14.4 is modified so that it copies the noise data into the byte array in preparation for loading into a texture object, as follows:

```
```cpp
void fillDataArray(GLubyte data[]) {
    for (int i=0; i<noiseWidth; i++) {
        for (int j=0; j<noiseHeight; j++) {
            for (int k=0; k<noiseDepth; k++) {
                data[(i*noiseWidth*noiseHeight*4)+(j*noiseHeight*4)+k*4+0] =
                    (GLubyte) (noise[i][j][k] % 256);
                data[(i*noiseWidth*noiseHeight*4)+(j*noiseHeight*4)+k*4+1] =
                    (GLubyte) (noise[i][j][k] % 256);
                data[(i*noiseWidth*noiseHeight*4)+(j*noiseHeight*4)+k*4+2] =
                    (GLubyte) (noise[i][j][k] % 256);
                data[(i*noiseWidth*noiseHeight*4)+(j*noiseHeight*4)+k*4+3] =
                    (GLubyte) 255;
            }
        }
    }
}
```
```

The rest of Program 14.4 for loading data into a texture object and applying it to a model is unchanged. We can view this 3D noise map by applying it to our simple cube model, as shown in Figure 14.12. In this example, noiseHeight = noiseWidth = noiseDepth = 256.

This is a 3D noise map, although it isn't a very useful one. As is, it is just *too* noisy to have very many practical applications. To make more practical, tunable noise patterns, we will replace the fillDataArray() function with different noise-producing procedures.

Suppose that we fill the data array by "zooming in" to a small subsection of the noise map illustrated in Figure 14.12, using indexes made smaller by integer division. The modification to the fillDataArray() function is shown below. The resulting 3D texture can be made more or less "blocky" depending on the "zooming" factor used to divide the index. In Figure 14.13, the textures show the result of zooming in by dividing the indices by zoom factors 8, 16, and 32 (left to right respectively).

![](bbox=[0.58, 0.68, 0.86, 0.82])

**Figure 14.12**
Cube textured with 3D noise data.