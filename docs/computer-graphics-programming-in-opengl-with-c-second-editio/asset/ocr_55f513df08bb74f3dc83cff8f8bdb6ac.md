```
```glsl
float bu3 = u * u * u;                   // u^3
float bv0 = (1.0-v) * (1.0-v) * (1.0-v); // (1-v)^3
float bv1 = 3.0 * v * (1.0-v) * (1.0-v); // 3v(1-v)^2
float bv2 = 3.0 * v * v * (1.0-v);       // 3v^2(1-v)
float bv3 = v * v * v;                   // v^3

// output the position of this vertex in the tessellated patch
vec3 outputPosition =
    bu0 * ( bv0*p00 + bv1*p01 + bv2*p02 + bv3*p03 )
  + bu1 * ( bv0*p10 + bv1*p11 + bv2*p12 + bv3*p13 )
  + bu2 * ( bv0*p20 + bv1*p21 + bv2*p22 + bv3*p23 )
  + bu3 * ( bv0*p30 + bv1*p31 + bv2*p32 + bv3*p33 );
gl_Position = mvp_matrix * vec4(outputPosition,1.0f);

// output the interpolated texture coordinates
vec2 tc1 = mix(texCoord_TCSout[0], texCoord_TCSout[3], gl_TessCoord.x);
vec2 tc2 = mix(texCoord_TCSout[12], texCoord_TCSout[15], gl_TessCoord.x);
vec2 tc = mix(tc2, tc1, gl_TessCoord.y);
texCoord_TESout = tc;
}
```
```

# ### Fragment Shader

```
```glsl
#version 430
in vec2 texCoord_TESout;
out vec4 color;
uniform mat4 mvp_matrix;
layout (binding = 0) uniform sampler2D tex_color;
void main(void)
{ color = texture(tex_color, texCoord_TESout);
}
```
```

# ### C++ / OpenGL application

```
```cpp
// This time we also pass a texture to paint the surface.
// Load the texture in init() as usual, then enable it in display()
void display(GLFWwindow* window, double currentTime) {

    glActiveTexture(GL_TEXTURE0);
    glBindTexture(GL_TEXTURE_2D, textureID);
    glFrontFace(GL_CCW);
    glPatchParameteri(GL_PATCH_VERTICES, 16);        // number of vertices per patch = 16
    glPolygonMode(GL_FRONT_AND_BACK, GL_FILL);
    glDrawArrays(GL_PATCHES, 0, 16);                 // total number of patch vertices: 16 x 1 patch = 16
}
```
```