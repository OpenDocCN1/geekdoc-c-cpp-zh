
![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_326_0.png)

**Figure 13.6** Geometry shader: primitive deletion.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_326_1.png)

**Figure 13.7** Primitive deletion showing back faces.

No other changes to the code are necessary. Note the use of the mod function—all vertices are passed through except those in the first of every three primitives, which are ignored. Here too, rendering the back-facing triangles can improve realism, as shown in Figure 13.7.

## 13.4 ADDING PRIMITIVES

Perhaps the most interesting and powerful use of geometry shaders is for adding additional vertices and/or primitives to a model being rendered. This makes it possible to do such things as increase the detail in an object to improve height mapping or to change the shape of an object completely.

Consider the following example, where we change each triangle in the torus to a tiny triangular pyramid.

Our strategy, similar to our previous “exploded” torus example, is illustrated in Figure 13.8. The vertices of an incoming triangle primitive are used to define the base of a pyramid. The walls of the pyramid are constructed of those vertices, and of a new point (called the “spike point”) computed by averaging the normals of the original vertices. New normal vectors are then computed for each of the three “sides” of the pyramid by taking the cross product of two vectors from the spike point to the base.

The geometry shader in Program 13.3 does this for each triangle primitive in the torus. For each incoming triangle, it outputs three triangle primitives, for a total of nine vertices. Each new triangle is built in the function makeNewTriangle(), which is called three times. It computes the normal for the specified triangle, then calls the function setOutputValues() to assign the appropriate output vertex attributes for each vertex emitted. After emitting all three vertices, it calls EndPrimitive(). To ensure that the lighting is performed accurately, new values of the light direction vector are computed for each newly created vertex.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_327_0.png)

**Figure 13.8** Converting triangles to pyramids.

### Program 13.3 Geometry: Add Primitives

```
...
vec3 newPoints[9], lightDir[9];
float sLen = 0.01;  // sLen is the "spike length", the height of the small pyramid

void setOutputValues(int p, vec3 norm)
{
    varyingNormal = norm;
    varyingLightDir = lightDir[p];
    varyingVertPos = newPoints[p];
    gl_Position = p_matrix * v_matrix * vec4(newPoints[p], 1.0);
}

void makeNewTriangle(int p1, int p2)
{  // generate surface normal for this triangle
    vec3 c1 = normalize(newPoints[p1] - newPoints[3]);
    vec3 c2 = normalize(newPoints[p2] - newPoints[3]);
    vec3 norm = cross(c1,c2);

    // generate and emit the three vertices
    setOutputValues(p1, norm); EmitVertex();
    setOutputValues(p2, norm); EmitVertex();
    setOutputValues(3, norm); EmitVertex();
    EndPrimitive();
}

void main(void)
{ // offset the three triangle vertices by the original surface normal
  vec3 sp0 = gl_in[0].gl_Position.xyz + varyingOriginalNormal[0]*sLen;
  vec3 sp1 = gl_in[1].gl_Position.xyz + varyingOriginalNormal[1]*sLen;
  vec3 sp2 = gl_in[2].gl_Position.xyz + varyingOriginalNormal[2]*sLen;

  // compute the new points comprising a small pyramid
  newPoints[0] = gl_in[0].gl_Position.xyz;
  newPoints[1] = gl_in[1].gl_Position.xyz;
  newPoints[2] = gl_in[2].gl_Position.xyz;
  newPoints[3] = (sp0 + sp1 + sp2)/3.0;              // spike point

  // compute the directions from the vertices to the light
  lightDir[0] = light.position - newPoints[0];
  lightDir[1] = light.position - newPoints[1];
  lightDir[2] = light.position - newPoints[2];
  lightDir[3] = light.position - newPoints[3];

  // build three new triangles to form a small pyramid on the surface
  makeNewTriangle(0,1);  // the third point is always the spike point
  makeNewTriangle(1,2);
  makeNewTriangle(2,0);
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_328_0.png)

**Figure 13.9** Geometry shader, primitive addition.

The resulting output is shown in Figure 13.9. If the spike length (sLen) variable is increased, the added surface “pyramids” would be taller. However, they could appear unrealistic in the absence of shadows. Adding shadow mapping to Program 13.3 is left as an exercise for the reader.

Careful application of this technique can enable the simulation of

```
vec3 op1 = gl_in[1].gl_Position.xyz;
vec3 op2 = gl_in[2].gl_Position.xyz;
vec3 ep0 = gl_in[0].gl_Position.xyz + varyingNormal[0]*sLen;    // offset triangle vertices
vec3 ep1 = gl_in[1].gl_Position.xyz + varyingNormal[1]*sLen;
vec3 ep2 = gl_in[2].gl_Position.xyz + varyingNormal[2]*sLen;

// compute the new points comprising a small line segment
vec3 newPoint1 = (op0 + op1 + op2)/3.0;    // original (start) point
vec3 newPoint2 = (ep0 + ep1 + ep2)/3.0;    // end point

gl_Position = p_matrix * v_matrix * vec4(newPoint1, 1.0);
varyingVertPosG = newPoint1;
varyingLightDirG = light.position - newPoint1;
varyingNormalG = varyingNormal[0];
EmitVertex();

gl_Position = proj_matrix * vec4(newPoint2, 1.0);
varyingVertPosG = newPoint2;
varyingLightDirG = light.position - newPoint2;
varyingNormalG = varyingNormal[1];
EmitVertex();

EndPrimitive();
}
```

## SUPPLEMENTAL NOTES

One of the appeals of geometry shaders is that they are relatively easy to use. Although many applications for which geometry shaders are used could be achieved using tessellation, the mechanism of geometry shaders often makes them easier to implement and debug. Of course, the relative fit of geometry versus tessellation depends on the particular application.

Generating convincing hair or fur is challenging, and there is a wide range of techniques employed depending on the application. In some cases, simple texturing is adequate and/or the use of tessellation or geometry shaders such as the basic technique shown in this chapter. When greater realism is required, movement (animation) and lighting become tricky. Two dedicated tools for hair and fur generation are *HairWorks* which is part of the NVIDIA GameWorks suite [GW21] and *TressFX* which was developed by AMD [TR21]. The former works with both OpenGL and DirectX, whereas the latter works only with DirectX. Examples of using TressFX can be found in [GP14].

## Exercises

- 13.1 Modify Program 13.1 so that it moves each vertex slightly toward the center of its primitive triangle. The result should look similar to the exploded torus in Figure 13.5, but without the overall change in torus size.
- 13.2 Modify Program 13.2 so that it deletes every other primitive, or every fourth primitive (rather than every third primitive), and observe the effect on the resulting rendered torus. Also, try changing the dimensionality of the instantiated torus to a value that is *not* a multiple of three (such as 40), while still deleting every third primitive. There are many possible effects.
- 13.3 (*PROJECT*) Modify Program 13.4 to additionally render the original torus. That is, render *both* a lighted torus (as previously done in Chapter 7) and the outgoing line segments (using a geometry shader) so that the “hair” looks like it is coming out of the torus.
- 13.4 (*PROJECT*) Modify Program 13.4 so that it produces outward-facing line segments with *more than two* vertices, arranged so as to make the line segments appear to bend slightly.

## References

- **[DV20]** J. deVries, *LearnOpenGL* (Kendall and Welling, 2020), accessed March 2021, http://www.learnopengl.com/
- **[GP14]** *GPU Pro 5: Advanced Rendering Techniques*, ed. W. Engel (CRC Press, 2014).
- **[GW21]** NVIDIA GameWorks Suite, 2018, accessed March 2021, https://developer.nvidia.com/gameworks
- **[KS16]** J. Kessenich, G. Sellers, and D. Shreiner, *OpenGL Programming Guide: The Official Guide to Learning OpenGL, Version 4.5 with SPIR-V*, 9th ed. (Addison-Wesley, 2016).
- **[TR13]** P. Trettner, *Prototype Grass* (blog), 2013, accessed July 2016, https://upvoid.com/devblog/2013/02/prototype-grass/
- **[TR21]** TressFX Hair, AMD, 2018, accessed March 2021, https://www.amd.com/en/technologies/tressfx
