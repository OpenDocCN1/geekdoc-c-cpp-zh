# ### Program 8.2 Percentage Closer Filtering (PCF)

Fragment Shader

```
~~~glsl
#version 430
// all variable declarations are unchanged
...
// Returns the shadow depth value for a texel at distance (x,y) from shadow_coord. Recall that
// shadow_coord is the location in the shadow map corresponding to the current pixel being rendered.
float lookup(float ox, float oy)
{
    float t = textureProj(shadowTex,
        shadow_coord + vec4(ox * 0.001 * shadow_coord.w, oy * 0.001 * shadow_coord.w,
        -0.01, 0.0));  // the third parameter (-0.01) is an offset to counteract shadow acne
    return t;
}

void main(void)
{
    float shadowFactor = 0.0;
    vec3 L = normalize(vLightDir);
    vec3 N = normalize(vNormal);
    vec3 V = normalize(-VertPos);
    vec3 H = normalize(vHalfVec);

    // ---- this section produces a 4-sample dithered soft shadow
    float swidth = 2.5;             // tunable amount of shadow spread
    // produces one of 4 sample patterns depending on gl_FragCoord mod 2
    vec2 offset = mod(floor(gl_FragCoord.xy), 2.0) * swidth;
    shadowFactor += lookup(1.5*swidth + offset.x, 1.5*swidth - offset.y);
    shadowFactor += lookup(1.5*swidth + offset.x, -0.5*swidth - offset.y);
    shadowFactor += lookup(-0.5*swidth + offset.x, 1.5*swidth - offset.y);
    shadowFactor += lookup(-0.5*swidth + offset.x, -0.5*swidth - offset.y);
    shadowFactor = shadowFactor / 4.0;  // shadowFactor is an average of the four sampled points

    // ---- this section, if un-commented, produces a 64-sample hi resolution soft shadow
    // float swidth = 2.5;          // tunable amount of shadow spread
    // float endp = swidth*3.0 + swidth/2.0;
    // for (float m=-endp; m<=endp; m+=swidth)
    //    for (float n=-endp; n<=endp; n+=swidth)
    //    {
    //        shadowFactor += lookup(m,n);
    //    }
    // shadowFactor = shadowFactor / 64.0;

    vec4 shadowColor = globalAmbient * material.ambient + light.ambient * material.ambient;
}
~~~
```