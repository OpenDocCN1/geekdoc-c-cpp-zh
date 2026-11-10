```
```glsl
#version 430
in vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;
in vec4 shadow_coord;
out vec4 fragColor;
// same structs and uniforms as in the vertex shader

void main(void)
{
    vec3 L = normalize(varyingLightDir);
    vec3 N = normalize(varyingNormal);
    vec3 V = normalize(varyingVertPos);
    vec3 H = normalize(varyingHalfVec);

    float inShadow = textureProj(shadow_coord);

    fragColor = globalAmbient * material.ambient + light.ambient * material.ambient;
    if (inShadow != 0.0)
    {
        fragColor += light.diffuse * material.diffuse * max(dot(L,N),0.0)
            + light.specular * material.specular
            * pow(max(dot(H,N),0.0),material.shininess*3.0);
    }
}
```
```

**Figure 8.7**  
Shadow mapping pass 2 fragment shader.

fragment shader as follows. The z component represents the distance from the light to the pixel. The (x,y) components are used to retrieve the depth information stored in the (2D) shadow texture. This retrieved value (the distance to the object nearest the light) is compared with Z. This comparison produces a “binary” result that tells us whether the pixel we are rendering is further from the light than the object nearest the light (i.e., whether the pixel is in shadow).

If in OpenGL we use glFramebufferTexture() as described earlier and we enable *depth testing*, then using a `sampler2DShadow` and `textureProj()` as shown in the fragment shader (Figure 8.7) will do exactly what we need. That is, `textureProj()` will output either 0.0 or 1.0 depending on the depth comparison. Based on this value, we can then in the fragment shader omit the diffuse and specular contributions when the pixel is further from the light than the object nearest the light, effectively creating the shadow when appropriate. An overview is shown in Figure 8.8.

We are now ready to build our JOGL application to work with the previously described shaders.