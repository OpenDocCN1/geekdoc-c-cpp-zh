```
void main()
{
// Calculate the coordinate to sample into the G-buffer
vec2 gbufferCoord = gl_FragCoord.xy / uScreenDimensions;

// Sample from G-buffer
vec3 gbufferDiffuse = texture(uGDiffuse, gbufferCoord).xyz;
vec3 gbufferNorm = texture(uGNormal, gbufferCoord).xyz;
vec3 gbufferWorldPos = texture(uGWorldPos, gbufferCoord).xyz;

// Calculate normal and vector from surface to light
vec3 N = normalize(gbufferNorm);
vec3 L = normalize(uPointLight.mWorldPos - gbufferWorldPos);
}
```