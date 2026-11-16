these methods so that we can understand and point out the advantages of the novel method that we will propose.

# NVIDIA's NvLink

The NvLink tool provided by NVIDIA is an older additive method used to sew together assembly language vertex shader fragments. The #beginfragment and #endfragment keywords are placed within the shader code to delimit fragments. The INVLink interface (obtained from a library provided by NVIDIA) can then be used to link the fragments together at runtime. We will not dwell more on this technique, as its restricted use for assembly shaders severely limits its usefulness; it is mostly of historic value.

# D3DX Fragment Linker

The D3DX fragment linker consists of a set of sparsely documented functions in the D3DX library. The key entrypoints are D3DXAssembleFragments(), LinkShader(), and LinkVertexShader(). These functions can be used to additionally link shader fragments written in DirectX assembly language or compiled from HLSL.

To use the linker, a semantic prefixed with _r is assigned to some function parameters. These parameters then act as the glue between the shader fragments, serving as their communication channel. The vertex fragment also has to be declared with a special vertexfragment keyword, as shown in the following example:

```
void Transform(
    float4 vPos : POSITION,
    float4 vNormal : NORMAL,
    float3 vPositionResult : _r_TransformedPosition,
    float4 vNormalResult : r_TransformedNormal )
{
    vPositionResult = mul( vPos, mWorldView );
    vNormalResult = mul( vNormal, (float3x3)mWorldView );
}
Vertexfragment Transform = compile_fragment vs_1_1 Transform();
```

D3DXAssembleFragments() can then be used to load all shader fragments from a given file, and LinkShader() can be used to combine them to construct shaders [Boyd].

Using the fragment linker is a lightweight process that can be done at runtime. The linker will resolve symbol tables, optimize register use, and remove dead code.

# Generating Shader Variants through HLSL

Since shaders can be written in a high-level language, it is only natural to use the shader compiler to concatenate shader code strings together to build a more complex shader. Generating shader variants through a high-level shader language can be done using either additive or subtractive methods.