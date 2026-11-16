The output of the vertex shader is the transformed position and the lit color value. The color value contains the pixel color and the depth in the alpha channel. The pixel shader program of impostor rendering is very simple. Since in this case, the alpha channel contains depth values, we have to disable alpha blending before executing this code.

```
void main( vertout IN,
           out float4 color : COLOR)
{
    color.rgba = IN.Col.rgba;
}
```

Mipmapping of impostors is unnecessary, because the impostor texels have the same orientation and approximately similar size as the pixels. The effect of rescaling the impostors due to perspective correction is not significant.

# ## Using the Impostor

The second pass that renders the tree canopy into the final image as a collection of impostors is far more interesting. The vertex shader is used to calculate the projected size and the position of the impostor texture. The application loads these values into the vertex shader constant store as if the impostor were located in the center of the foliage. The vertex program makes the appropriate corrections based on the actual location of the leaf cloud in the image and passes the associated depth value to the pixel shader. The pixel shader is responsible for rendering the impostor texture, including correct depth information.

Two triangles are needed to draw each impostor to the screen. At first, the vertex shader calculates the impostor center. The impostor texture contains the depth of leaves from the impostor’s front clipping plane. Thus, we add the z distance of the leaf cloud to the z coordinates stored in the impostor. Additionally, the impostor is scaled according to the perspective distortion.

```
vertout main(appin IN,
             uniform float4x4 ModelView,
             uniform float4x4 Proj,
             uniform float4 constans,
             uniform float impostorSize,
             uniform float centerBlockSize,
             uniform float impostorZSize,
             )
{
    vertout OUT;

    float4 pos = IN.Pos.xyzz;
    pos.w = 1;
}
```