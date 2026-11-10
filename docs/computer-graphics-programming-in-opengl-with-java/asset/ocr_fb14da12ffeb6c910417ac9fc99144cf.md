# Fragment Shader

```
```glsl
...
in vec2 tes_out;
out vec4 color;
layout (binding = 0) uniform sampler2D tex_color;
void main(void)
{ color = texture(tex_color, tes_out);
}
```
```

The fragment shader is similar to the one for Program 12.2 and simply outputs the color based on the texture image. The Java/JOGL application is essentially unchanged—it loads the texture (serving as both the texture and height map) and enables a sampler for it. Figure 12.6 shows the texture image (on the left) and the final output of this first attempt, which unfortunately does not yet achieve proper height mapping.

The first results are severely flawed. Although we can now see silhouette detail on the far horizon, the bumps there don't correspond to the actual detail in the texture map. Recall that in a height map, white is supposed to mean “high” and black is supposed to mean “low.” The area at the upper right, in particular, shows large hills that bear no relation to the light and dark colors in the image.

![](bbox=[0.201, 0.541, 0.797, 0.845])

**Figure 12.6**
Tessellated terrain—failed first attempt, with insufficient number of vertices.