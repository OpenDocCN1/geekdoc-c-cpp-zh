# Vertex shader:

```
```glsl
...
uniform mat4 texRot_matrix;
void main(void)
{
    ...
    originalPosition = vec3(texRot_matrix * vec4(position,1.0)).xyz;
    ...
}
```
```

# Fragment shader:

```
```glsl
...
void main(void)
{
    ...
    uniform mat4 texRot_matrix;
    ...
    // combine lighting with 3D texturing
    fragColor =
        0.5 * (...)
        +
        0.5 * texture(s,originalPosition / 2.0 + 0.5);
}
```
```

![](bbox=[0.144, 0.56, 0.494, 0.691])

Figure 14.20
Dolphin textured with 'wood' 3D noise map.

The resulting 3D textured wood dolphin is shown in Figure 14.20. There is one additional detail in the fragment shader worth noting. Since we are rotating the model within a 3D texture, it is sometimes possible for this to cause the vertex positions to move beyond the typical [0..1] range of texture coordinates as a result of the rotation. If this were to happen, we could adjust for this possibility by dividing the original vertex positions by a larger number (such as 4.0 rather than 2.0), and then adding a slightly larger number (such as 0.6) to center it in the texture space. Since our noise map wraps, vertex coordinates that move beyond the [0..1] range do not cause a problem.