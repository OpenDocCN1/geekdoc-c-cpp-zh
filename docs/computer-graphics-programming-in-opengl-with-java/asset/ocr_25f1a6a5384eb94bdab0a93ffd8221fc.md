```
```glsl
void main(void)
{ // Include this pass-through of original vertex for interpolation:
    originalVertex = vertex;
    ...
}
```
```

# ### Fragment Shader

```
```glsl
#version 430
// same as Phong shading, but add this input vertex attribute:
in vec3 originalVertex;
...
void main(void)
{
    ...
    //add the following to perturb the incoming normal vector:
    float a = 0.25;                 // a controls height of bumps
    float b = 100.0;                // b controls width of bumps
    float x = originalVertex.x;
    float y = originalVertex.y;
    float z = originalVertex.z;
    N.x = varyingNormal.x + a*sin(b*x);  // perturb incoming normal using sine function
    N.y = varyingNormal.y + a*sin(b*y);
    N.z = varyingNormal.z + a*sin(b*z);
    N = normalize(N);
    // lighting computations and output fragColor (unchanged) now utilize the perturbed normal N
    ...
}
```
```

# ## 10.2 NORMAL MAPPING

An alternative to bump mapping is to replace the normals using a lookup table. This allows us to construct bumps for which there is no mathematical function, such as the bumps corresponding to the craters on the moon. A common way of doing this is called *normal mapping*.

To understand how this works, we start by noting that a vector can be stored to reasonable precision in three bytes, one for each of the X, Y, and Z components. This makes it possible to store normals in a color image file, with the R, G, and B components corresponding to X, Y, and Z. RGB values in an image are stored in