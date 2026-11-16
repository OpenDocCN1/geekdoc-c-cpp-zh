
![](img/672fe9a2d008ba627b1991e15d70f43e_581_0.png)

![](img/672fe9a2d008ba627b1991e15d70f43e_581_1.png)

impostors updated every frame instead of static sprites successfully eliminates this problem.

In the stage of impostor rendering, depth and color information are stored in target textures. The result is a 2.5 dimensional impostor. The z-near and z-far planes are adjusted to approximate a reasonable bounding box for the rendered group of leaves, as shown in Figure 5.4.6. In the final phase of rendering, the stored depth values are appropriately scaled and clipped to the final depth buffer before depth testing is performed, yielding a volumetric feel to the textured sprites, which can overlap in a spatially coherent manner. The artificial look resulting from repetition of the same image over many sprites is almost completely eliminated, as volumetric overlapping obscures this arrangement to the point where it is almost impossible to discern any single impostor.

## Implementation

The proposed technique produces very convincing results and can be efficiently implemented using the GPU of recent video cards, as shown schematically in Figure 5.4.7. Figure 5.4.8 shows the tree canopy rendered using impostors.

![](img/672fe9a2d008ba627b1991e15d70f43e_582_0.png)

FIGURE 5.4.7 Block diagram for implementation using two vertex and two pixel shaders.

The implementation assumes Version 2.0 vertex and pixel shaders and uses only standard techniques. The code is written in C++ with DirectX 9 [Microsoft04]. The shader program is written in Cg [NVIDIA02]. The example program shows a tree equivalent to 1.6 million polygons.

Leaves are rendered into an impostor texture at the resolution of the final image to avoid resizing artifacts and performance overhead. Allocating impostor textures every frame would have large performance overhead, thus it is recommended that applications pre-allocate big enough impostor textures for all cases.

![](img/672fe9a2d008ba627b1991e15d70f43e_583_0.png)

FIGURE 5.4.8 Tree canopy rendered using impostors.

## Depth Precision

Current graphics cards do not provide efficient access to the depth buffer because of internal optimization considerations. Because of this, the pixel program of the first pass stores depth information in the alpha channel, thus enabling the next stage to access it. Since the alpha channel has 8-bit precision, the projection matrix should be set carefully to minimize information loss.

The front clipping plane is moved to the front of the leaf cloud, and the far clipping plane is moved to its back. Additionally, the center of the window is moved to the center of the foliage. In the Direct3D rendering pipeline, the corresponding projection matrix is [Szirnay95]:

```
M'_{p_v} = \begin{bmatrix} w' & 0 & 0 & 0 \\ 0 & h' & 0 & 0 \\ x_{offset} & y_{offset} & \frac{z'_f}{z'_f - z'_n} & 1 \\ 0 & 0 & \frac{-z'_f z'_n}{z'_f - z'_n} & 0 \end{bmatrix}
```

$w' = w \cdot a_{impostor}
$h' = w' \cdot a_{impostorXY}
$z'_n = z_{center} - r_{impostor}
$z'_f = z_{center} + r_{impostor}

where $w$ is the half window width (which can be computed from the horizontal field of view as $w = 1 / \tan(fov / 2)$), $a_{impostor}$ is the ratio of the number of pixel columns in the frame buffer, and in the impostor texture, $z_{center}$ is distance along axis $z$ between the eye position and the center of the foliage, and $r_{impostor}$ is the radius of leaf cloud.

To move the leaf cloud to the center of the impostor texture, $x_{offset}$ and $y_{offset}$ are determined. These values are calculated by transforming the center of the foliage with the standard model, view, and projection transformations, which determines the center of the foliage in screen coordinates. The computed $x_{offset}$ and $y_{offset}$ values are the first two screen coordinates multiplied by -1.

## Rendering the Impostors

As mentioned earlier, this rendering algorithm has two passes. The first pass computes the impostors and uses the following vertex shader:

```
vertout main(appin IN,
    uniform float4x4
    uniform float4
    uniform float4
{
    vertout OUT;

    float4 pos = IN.Pos.xyzz;
    pos.w = 1;

    pos = mul(pos, mModelViewProj);
    pos /= pos.w;

    OUT.Pos = pos;
    OUT.Col.a = pos.z;

    float light = max(0, dot(IN.Normal.xyz, invTrSunDir.xyz));
    OUT.Col.rgb = IN.Col * (light * colorParam.x + colorParam.y);

    return OUT;
}
```

The leaf cloud will be rendered into the impostor using this vertex shader. Each vertex has a position, normal, and color. The vertex shader also gets two additional parameters defining the direction of the sun and its directional and ambient intensities. The diffuse illumination model is applied to compute the reflected intensity.

The output of the vertex shader is the transformed position and the lit color value. The color value contains the pixel color and the depth in the alpha channel. The pixel shader program of impostor rendering is very simple. Since in this case, the alpha channel contains depth values, we have to disable alpha blending before executing this code.

```
void main( vertout IN,
           out float4 color : COLOR)
{
    color.rgba = IN.Col.rgba;
}
```

Mipmapping of impostors is unnecessary, because the impostor texels have the same orientation and approximately similar size as the pixels. The effect of rescaling the impostors due to perspective correction is not significant.

### Using the Impostor

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
// calculate center point of the impostor from view
Pos    = mul( pos, ModelView);
float4 scl = float4( 0, ImpostorSize, pos.z, 1);

// projection transformation
pos    = mul( pos, Proj);
pos    /= pos.w;
pos.z  -= impostorZSize;

// calculate size of the impostor
scl    = mul( scl, Proj);
scl    /= scl.w;

// calculate scale factor
float scale = scl.x / centerBlockSize;

// calculate impostor corner
float2 uvp   = (IN.uv - 0.5) * constans.xy * scale;
pos    = pos + float4( uvp.x, uvp.y, 0, 0);

// calculate impostor uv parameter
float2 uv   = IN.uv * constans.z + constans.w;

OUT.Pos   = pos;
OUT.Col.rgb = IN.Col;
OUT.Col.w   = 0;
OUT.uv.w   = float4( uv.x, uv.y, pos.z, 1);

return OUT;
}
```

The pixel program has to determine the real depth of impostor texels and ignore any invisible ones. If the scaled z value of a texel is greater than 1, it is not visible. Current pixel shaders do not support pixel pipeline breaking, thus the final depth values of these invisible texels have to be set big enough to let the z-buffer hardware ignore them. The pixel shader gets constant depthScale, which scales the depth values of the impostors. Finally, the scaled depth value is added to the depth of the front clipping plane used in the impostor computation.

```
void main( vertout IN,
           uniform sampler2D impostorTexture,
           uniform float depthScale,
           out float4 color,
           out float depth : DEPTH)
{
    float4 texCol = tex2D(impostorTexture, IN.uv.xy);
    if (texCol.a >= 1.f) {
        depth = 1;
    } else {
        depth = IN.uv.z + texCol.a * depthScale;
    }
    color.xyz = texCol.xyz * IN.Col.xyz;
    color.a   = 1;
}
```
