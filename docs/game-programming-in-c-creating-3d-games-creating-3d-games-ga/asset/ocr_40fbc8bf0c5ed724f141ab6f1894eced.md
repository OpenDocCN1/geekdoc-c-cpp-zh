```
```glsl
// Compute Phong diffuse component for the light
vec3 Phong = vec3(0.0, 0.0, 0.0);
float NdotL = dot(N, L);
if (NdotL > 0)
{
    // Get the distance between the light and the world pos
    float dist = distance(uPointLight.mWorldPos, gbufferWorldPos);
    // Use smoothstep to compute value in range [0,1]
    // between inner/outer radius
    float intensity = smoothstep(uPointLight.mInnerRadius,
                                    uPointLight.mOuterRadius, dist);
    // The diffuse color of the light depends on intensity
    vec3 DiffuseColor = mix(uPointLight.mDiffuseColor,
                            vec3(0.0, 0.0, 0.0), intensity);
    Phong = DiffuseColor * NdotL;
}
// Final color is texture color times phong light
outColor = vec4(gbufferDiffuse * Phong, 1.0);
}```
```