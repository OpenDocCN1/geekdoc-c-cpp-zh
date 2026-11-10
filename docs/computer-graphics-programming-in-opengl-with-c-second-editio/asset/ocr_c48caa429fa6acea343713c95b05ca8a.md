![](bbox=[0.14, 0.112, 0.854, 0.309])

**Figure 10.7**
Normal map lighting effects on the moon.

![](bbox=[0.14, 0.379, 0.854, 0.572])

**Figure 10.8**
Texturing plus normal mapping, with lighting from the left and right.

light source (or camera or object movement). Lighting in the two images is from the left and right sides respectively.

Our program now requires two textures—one for the moon surface image, and one for the normal map—and thus two samplers. The fragment shader blends the texture color with the color produced by the lighting computation as shown in Program 10.3, using the technique described previously in Section 7.6.

# ### *Program 10.3 Texturing plus Normal Map*

```
```c
// variables and structs as in previous fragment shader, plus:
layout (binding=0) uniform sampler2D s0;      // normal map
layout (binding=1) uniform sampler2D s1;      // texture
```
```