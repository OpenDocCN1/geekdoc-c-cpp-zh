# ### Program 12.5 Tessellation Level of Detail (LOD)

# #### Tessellation Control Shader

```
    ...
    void main(void)
    {
        float subdivisions = 16.0;                 // tunable constant based on density of detail in height map
        if (gl_InvocationID == 0)
        {
            vec4 p0 = mvp * gl_in[0].gl_Position;      // control pt. positions in screen space
            vec4 p1 = mvp * gl_in[1].gl_Position;
            vec4 p2 = mvp * gl_in[2].gl_Position;
            p0 = p0 / p0.w;
            p1 = p1 / p1.w;
            p2 = p2 / p2.w;
            float width = length(p2.xy - p0.xy) * subdivisions + 1.0;   // perceived "width" of tess grid
            float height = length(p1.xy - p0.xy) * subdivisions + 1.0;  // perceived "height" of tess grid
            gl_TessLevelOuter[0] = height;             // set tess levels based on perceived side lengths
            gl_TessLevelOuter[1] = width;
            gl_TessLevelOuter[2] = height;
            gl_TessLevelOuter[3] = width;
            gl_TessLevelInner[0] = width;
            gl_TessLevelInner[1] = height;
        }
        // forward texture coordinates and control points to TES as before
        tcs_out[gl_InvocationID] = tcs_in[gl_InvocationID];
        gl_out[gl_InvocationID].gl_Position = gl_in[gl_InvocationID].gl_Position;
    }
```

Applying these control shader changes to the instance (but not lighted) version of our scene from Figure 12.7, and replacing the height map with Hastings-Trew's more finely tuned version shown in Figure 12.8 produces the improved scene, with more realistic horizon detail, shown in Figure 12.10.

In this example it is also useful to change the layout specifier in the evaluation shader from:

```
    layout (quads, equal_spacing, cw) in
```

![](bbox=[0.49, 0.571, 0.857, 0.819])

**Figure 12.10**
Tessellated moon with controlled level of detail (LOD).