Unlike 2D textures, which can be built from standard image files, 3D textures are usually generated *procedurally*. As was done previously for 2D textures, we decide on a resolution—that is, the number of texels in each dimension. Depending on the colors in the texture, we may build a three-dimensional array containing those colors. Alternatively, if the texture holds a “pattern” that could be utilized with various colors, we might instead build an array that holds the pattern, such as with 0s and 1s.

For example, we can build a 3D texture that represents horizontal stripes by filling an array with 0s and 1s corresponding to the desired stripe pattern. Suppose that the desired resolution of the texture is 200x200x200 texels and the texture comprises alternating stripes that are each 10 texels high. A simple function that builds such a structure by filling an array with appropriate 0s and 1s in a nested loop (assuming in this case that width, height, and depth variables are each set to 200), would be as follows:

```
```cpp
void generate3Dpattern()
{
    for (int x=0; x<texWidth; x++)
    {
        for (int y=0; y<texHeight; y++)
        {
            for (int z=0; z<texDepth; z++)
            {
                if ((y/10) % 2 == 0)
                    tex3Dpattern[x][y][z] = 0.0;
                else
                    tex3Dpattern[x][y][z] = 1.0;
            }
        }
    }
}
```
```

The pattern stored in the tex3Dpattern array is illustrated in Figure 14.8, with the 0s rendered in blue and the 1s rendered in yellow.

Texturing an object with the above striped pattern requires the following steps:

+   1. Generating the pattern as already shown
+   2. Using the pattern to fill a byte array of desired colors
+   3. Loading the byte array into a texture object

![](bbox=[0.6, 0.7, 0.86, 0.88])

**Figure 14.8**
Striped 3D texture pattern.