| | Position | | | Normal | | | Bones | Wt | UV | |
|---|---|---|---|---|---|---|---|---|---|---|---|
| x | y | z | x | y | z | [4] | [4] | u | v |
| 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 |

```
Offset to Normal = sizeof(float) * 3
Offset to Bones = sizeof(float) * 6
Offset to Bone Weights = sizeof(float) * 6 + 4
Offset to UV = sizeof(float) * 6 + 8
Stride = sizeof(float) * 8 + sizeof(char) * 8
```

# Figure 12.3 Vertex layout with bone influences and weights

To reduce the memory usage of `inSkinBones` and `inSkinWeights`, you don't need to make any further changes to the shader code. Instead, you need to specify the expected sizes of these attributes when defining the vertex array attributes in your C++ code. Recall from Chapter 5, “OpenGL,” that the definition of the vertex array attributes occurs in the VertexArray constructor. To support different types of vertex layouts, you add a new enum to the declaration of the `VertexArray` class in `VertexArray.h`:

```
enum Layout
{
    PosNormTex,
    PosNormSkinTex
};
```