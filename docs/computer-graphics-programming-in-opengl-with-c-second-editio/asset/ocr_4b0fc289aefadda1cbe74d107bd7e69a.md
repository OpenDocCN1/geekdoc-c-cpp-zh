```
~~~glsl
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;

layout(binding=0) uniform sampler2D t;      // for texture
layout(binding=1) uniform sampler2D h;      // for heightmap

void main(void)
{  // "p" is the vertex position altered by the height map.
   // Since the height map is grayscale, any of the color components can be
   // used (we use "r"). Dividing by 5.0 is to adjust the height.
   vec4 p = vec4(vertexPos, 1.0) + vec4((normal * (texture(h, texCoord).r) / 5.0f), 1.0f);
   tc = tex_coord;
   gl_Position = proj_matrix * mv_matrix * p;
}
~~~
```

Figure 10.14 shows a simple height map (top left) created by scribbling in a paint program. A white square is also drawn in the height map image. A green-tinted version of the height map (bottom left) is used as a texture. When the height map is applied to a rectangular 100x100 grid model using the shader shown in Program 10.4, it produces a sort of "terrain" (shown on the right). Note how the white square results in the precipice at the right.

Figure 10.15 shows another example of doing height mapping in a vertex shader. This time the height map is an outline of the continents of the world [HT12]. It is applied to a sphere textured with a blue-tinted version of the height map.

![](bbox=[0.14, 0.607, 0.863, 0.878])

**Figure 10.14**
Terrain: height-mapped in the vertex shader.