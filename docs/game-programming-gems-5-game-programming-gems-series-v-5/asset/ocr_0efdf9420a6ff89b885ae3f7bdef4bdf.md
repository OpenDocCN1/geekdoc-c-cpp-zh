```
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