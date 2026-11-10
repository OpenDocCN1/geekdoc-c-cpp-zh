We now are ready to implement our torus with positional lighting, using Phong shading. Most of the code is identical to that used for Gouraud shading. Since the C++/OpenGL code is unchanged, we present only the revised vertex and fragment shaders, shown in Program 7.2. Examining the output of Program 7.2, as shown in Figure 7.12, Phong shading corrects the artifacts present in Gouraud shading.

![](bbox=[0.543, 0.11, 0.857, 0.278])

**Figure 7.12**  
Torus with Phong shading.

# Program 7.2 Torus with Phong Shading

# Vertex Shader

```
```glsl
#version 430
layout (location=0) in vec3 vertPos;
layout (location=1) in vec3 vertNormal;
out vec3 varyingNormal;       // eye-space vertex normal
out vec3 varyingLightDir;     // vector pointing to the light
out vec3 varyingVertPos;      // vertex position in eye space

// structs and uniforms same as for Gouraud shading
...
void main(void)
{  // output vertex position, light direction, and normal to the rasterizer for interpolation
   varyingVertPos=(mv_matrix * vec4(vertPos,1.0)).xyz;
   varyingLightDir = light.position - varyingVertPos;
   varyingNormal=(norm_matrix * vec4(vertNormal,1.0)).xyz;

   gl_Position=proj_matrix * mv_matrix * vec4(vertPos,1.0);
}
```
```

# Fragment Shader

```
```glsl
#version 430
in vec3 varyingNormal;
in vec3 varyingLightDir;
in vec3 varyingVertPos;
out vec4 fragColor;

// structs and uniforms same as for Gouraud shading
...
```
```