![](bbox=[0.185, 0.085, 0.515, 0.335])

![](bbox=[0.595, 0.085, 0.935, 0.335])

![](bbox=[0.405, 0.355, 0.745, 0.605])

# FIGURE 5.1.3 (a) The eight octaves noise texture. (b) The same noise texture after we subtracted the cloud cover value and clamped it. (c) The same noise texture, after exponentiation. Notice how it starts to look like clouds.

The following HLSL code performs the computations described earlier (the rest of the shader will be given later in the article):

```
01. float cloud_cover = 0.45f;
02. float clouds_sharpness = 0.94f;
03. float3 tex = tex2D(Octave0, uv * OctavesScales0.x) *
OctavesWeights0.x;
04. tex += tex2D(Octave1, uv * OctavesScales0.y) *
OctavesWeights0.y;
05. tex += tex2D(Octave2, uv * OctavesScales0.z) *
OctavesWeights0.z;
06. tex += tex2D(Octave3, uv * OctavesScales0.w) *
OctavesWeights0.w;
07. tex += tex2D(Octave4, uv * OctavesScales1.x) *
OctavesWeights1.x;
```