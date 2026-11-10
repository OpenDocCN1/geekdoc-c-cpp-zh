
that some of the vertices participate in more than one triangle, and in those cases different texture coordinates might be used.

The values colored green (starting with “vn”) are the various normal vectors. This list too is often longer than the list of vertices (although not in this example), again because some of the vertices participate in more than one triangle, and in those cases different normal vectors might be used.

The values colored purple (starting with “f”), near the bottom of the file, specify the triangles (i.e., “faces”). In this example, each face (triangle) has three elements, each with three values separated by “/” (OBJ allows other formats as well). The values for each element are indices into the lists of vertices, texture coordinates, and normal vectors, respectively. For example, the third face is

```
f 2/7/3 5/8/3 3/9/3
```

This indicates that the second, fifth, and third vertices from the list of vertices (in blue) comprise a triangle (note that OBJ indices start at 1). The corresponding texture coordinates are the seventh, eighth, and ninth from the list of texture coordinates in the section colored red. All three vertices have the same normal vector, the third in the list of normals in the section colored green.

Models in OBJ format are not required to have normal vectors, or even texture coordinates. If a model does not have texture coordinates or normals, the face values would specify only the vertex indices:

```
f 2 5 3
```

If a model has texture coordinates, but not normal vectors, the format would be as follows:

```
f 2/7 5/8 3/9
```

And, if the model has normals but not texture coordinates, the format would be

```
f 2//3 5//3 3//3
```

It is not unusual for a model to have tens of thousands of vertices. There are hundreds of such models available for download on the Internet for nearly every conceivable application, including models of animals, buildings, cars, planes, mythical creatures, people, and so on.

Programs of varying sophistication that can import an OBJ model are available on the Internet. Alternatively, it is relatively easy to write a very simple OBJ loader function that can handle the basic tags we have seen (v, vt, vn, and f). Program 6.3 shows one such loader, albeit a *very* limited one. It incorporates a class to hold an arbitrary imported model, which in turn calls the importer.

Before we describe the code in our simple OBJ importer, we must warn the reader of its limitations:

- It only supports models that include *all three* face attribute fields. That is, vertex positions, texture coordinates, and normals *must all* be present and in the form f ###/###/###.
- The material tag, often used to specify a texture file, is ignored—texturing must be done using the methods described in Chapter 5.
- Only OBJ models comprising a single triangle mesh are supported (the OBJ format supports models comprised of multiple meshes, but our simple importer does not).
- It assumes that elements on each line are separated by exactly one space.

If you have an OBJ model that doesn’t satisfy all of the above criteria and you wish to import it using the simple loader in Program 6.3, it *may* still be feasible to do so. It is often possible to load such a model into Blender, and then export it to another OBJ file that accommodates the loader’s limitations. For instance, if the model doesn’t include normal vectors, it is possible to have Blender produce normal vectors while it exports the revised OBJ file.

Another limitation of our OBJ loader has to do with indexing. Observe in the previous descriptions that the “face” tag allows for the possibility of mix-and-matching vertex positions, texture coordinates, and normal vectors. For example, two different “face” rows may include indices which point to the same v entry, but different vt entries. Unfortunately, OpenGL’s indexing mechanism does not support this level of flexibility—index entries in OpenGL can only point to a particular vertex *along with its attributes*. This complicates writing an OBJ model loader somewhat, as we cannot simply copy the references in the triangle face entries into an index array. Rather, using OpenGL indexing would require ensuring that entire *combinations* of v, vt, and vn values for a face entry each have their own references in the index array. A simpler, albeit less efficient, alternative is to create a new vertex for every triangle face entry. We opt for this simpler approach here in the interest of clarity, despite the space-saving advantage of using OpenGL indexing (especially when loading larger models).

The ModelImporter class includes a parseOBJ() function that reads in each line of an OBJ file one-by-one, handling separately the four cases v, vt, vn, and f. In each case, the subsequent numbers on the line are extracted, first by using substring() to skip the initial v, vt, vn, or f character(s) and then using the iterator returned by the split() function to extract each subsequent parameter value, storing them in an ArrayList. As the face (f) entries are processed, the vertices are built, with corresponding entries in parallel arrays for vertex positions, texture coordinates, and normal vectors.

The ModelImporter class is embedded in the ImportedModel class, which simplifies loading and accessing the vertices of an OBJ file by putting the imported vertices into arrays of Vector3f and Vector2f objects. Recall these are JOML classes; we use them here to store vertex positions, texture coordinates, and normal vectors. The accessors in the ImportedModel class then make them available to the Java/JOGL application in much the same manner as was done in the Sphere and Torus classes.

Following the ModelImporter and ImportedModel classes is an example sequence of calls for loading an OBJ file and then transferring the vertex information into a set of VBOs for subsequent rendering.

Figure 6.16 shows a rendered model of the space shuttle, downloaded as an OBJ file from the NASA website [NA21], imported using the code from Program 6.3 and textured using the code from Program 5.1 with the associated NASA texture image file, with anisotropic filtering. This texture image is an example of the use of *UV-mapping*, where texture coordinates in the model are carefully mapped to particular regions of the texture image. (As mentioned in *Chapter 5*, the details of *UV-mapping* are outside the scope of this book.)

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_174_0.png)

**Figure 6.16**
NASA space shuttle model with texture.

## Program 6.3 Simple (Limited) OBJ Loader

### ImportedModel class

```java
public class ImportedModel
{
  private Vector3f[] vertices;
  private Vector2f[] texCoords;
  private Vector3f[] normals;
  private int numVertices;

  public ImportedModel(String filename)
  {
    ModelImporter modelImporter = new ModelImporter();
    try
    {
      modelImporter.parseOBJ(filename);    // uses modelImporter to get vertex information
      numVertices = modelImporter.getNumVertices();
      float[] verts = modelImporter.getVertices();
      float[] tcs = modelImporter.getTextureCoordinates();
      float[] norms = modelImporter.getNormals();

      vertices = new Vector3f[numVertices];
      texCoords = new Vector2f[numVertices];
      normals = new Vector3f[numVertices];

      for(int i=0; i<vertices.length; i++)
      {
        vertices[i] = new Vector3f();
        vertices[i].set(verts[i*3], verts[i*3+1], verts[i*3+2]);
        texCoords[i] = new Vector2f();
        texCoords[i].set(tcs[i*2], tcs[i*2+1]);
        normals[i] = new Vector3f();
        normals[i].set(norms[i*3], norms[i*3+1], norms[i*3+2]);
      }
    } catch (IOException e)
    {
      e.printStackTrace();
    }
  }

  public int getNumVertices() { return numVertices; }    // accessors
  public Vector3f[] getVertices() { return vertices; }
  public Vector2f[] getTexCoords() { return texCoords; }
  public Vector3f[] getNormals() { return normals; }
}
```

### ModelImporter nested class

```java
private class ModelImporter
{  // values as read in from OBJ file
   private ArrayList<Float> vertVals = new ArrayList<Float>();
   private ArrayList<Float> stVals = new ArrayList<Float>();
   private ArrayList<Float> normVals = new ArrayList<Float>();
```
