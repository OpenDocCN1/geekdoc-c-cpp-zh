the dot product is negative, max selects 0.

# Listing 6.12 Phong.frag Main Function

Click here to view code image

```
void main()
{
    // Surface normal
    vec3 N = normalize(fragNormal);
    // Vector from surface to light
    vec3 L = normalize(-uDirLight.mDirection);
    // Vector from surface to camera
    vec3 V = normalize(uCameraPos - fragWorldPos);
    // Reflection of -L about N
    vec3 R = normalize(reflect(-L, N));
    // Compute phong reflection
    vec3 Phong = uAmbientLight;
    float NdotL = dot(N, L);
    if (NdotL > 0)
    {
        vec3 Diffuse = uDirLight.mDiffuseColor * NdotL;
```