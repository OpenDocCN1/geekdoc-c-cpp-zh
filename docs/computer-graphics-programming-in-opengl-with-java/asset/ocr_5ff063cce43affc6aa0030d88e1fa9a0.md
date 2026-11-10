that some of the vertices participate in more than one triangle, and in those cases
different texture coordinates might be used.

The values colored green (starting with “vn”) are the various normal vectors.
This list too is often longer than the list of vertices (although not in this example),
again because some of the vertices participate in more than one triangle, and in
those cases different normal vectors might be used.

The values colored purple (starting with “f”), near the bottom of the file, specify
the triangles (i.e., “faces”). In this example, each face (triangle) has three elements,
each with three values separated by “/” (OBJ allows other formats as well). The
values for each element are indices into the lists of vertices, texture coordinates,
and normal vectors, respectively. For example, the third face is

```
```
f 2/7/3 5/8/3 3/9/3
```
```

This indicates that the second, fifth, and third vertices from the list of vertices
(in blue) comprise a triangle (note that OBJ indices start at 1). The corresponding
texture coordinates are the seventh, eighth, and ninth from the list of texture coordi-
nates in the section colored red. All three vertices have the same normal vector,
the third in the list of normals in the section colored green.

Models in OBJ format are not required to have normal vectors, or even texture
coordinates. If a model does not have texture coordinates or normals, the face
values would specify only the vertex indices:

```
```
f 2 5 3
```
```

If a model has texture coordinates, but not normal vectors, the format would
be as follows:

```
```
f 2/7 5/8 3/9
```
```

And, if the model has normals but not texture coordinates, the format
would be

```
```
f 2//3 5//3 3//3
```
```

It is not unusual for a model to have tens of thousands of vertices. There are
hundreds of such models available for download on the Internet for nearly every
conceivable application, including models of animals, buildings, cars, planes,
mythical creatures, people, and so on.