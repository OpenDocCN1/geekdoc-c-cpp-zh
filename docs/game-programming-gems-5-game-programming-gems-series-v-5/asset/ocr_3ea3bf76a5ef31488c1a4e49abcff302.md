```
// Compute some "random" texture coordinates depending on the
// position and view vector, which are used to look up into a
// noise texture in the pixel shader.
o.noiseUV.x = fmod(abs(dot(pos.yz, float3(1, 1, 1))), 2.0);
o.noiseUV.y = fmod(abs(2.0 * dot(v, float3(1, 1, 1))), 2.0);

return o;
}
```

Following is a flare pixel shader:

```
sampler tFlare;        // flare texture
sampler tNoise;        // 2D noise texture
sampler tScreen;       // back buffer contents

float flareIntensity;

struct PsInput
{
    float2 uv          : TEXCOORD0;
    float2 noiseUV     : TEXCOORD1;
    float2 screenUV    : TEXCOORD2;
};
```

```
float4 main(PsInput i) : COLOR
{
    // Sample flare texture
    float Alpha = tex2D(tFlare, i.uv);

    // Get noise value for flare intensity
    float noise = tex2D(tNoise, i.noiseUV);
    noise = lerp(0.6, 1.0, noise);

    // Get screen luminance at flare center
    float3 cScreen = tex2D(tScreen, i.screenUV);
    float lum = dot(cScreen, float3(0.3, 0.59, 0.11));

    // Discard fragment if luminance is less then 0.8
    clip(lum - 0.8);

    // Pull luminance for visible flares into [0, 1] range
    // and apply a gamma
    lum = smoothstep(0.8, 1.0, lum);
    lum *= lum;

    float4 o = 0;
    o.rgb = noise * lum * fAlpha * flareIntensity;
    return o;
}
```