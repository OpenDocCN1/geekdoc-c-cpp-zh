arbitrary shapes in 3D space and automatically produce the vertices, texture coordinates, vertex normals, and so on. There are too many such tools to list, but some examples are Maya, Blender, Lightwave, and Cinema4D, among many others. Blender is free and open source. Figure 6.13 shows an example Blender screen during the editing of a 3D model.

![](bbox=[0.167, 0.239, 0.833, 0.559])

In order for us to use a DCC-created model in our OpenGL scenes, that model needs to be saved (exported) in a format that we can read (import) into our program. There are several standard 3D model file formats; again, there are too many to list, but some examples are Wavefront (.obj), 3D Studio Max (.3ds), Stanford Scanning Repository (.ply), and Ogre3D (.mesh), to name a few. Arguably the simplest is Wavefront (usually dubbed OBJ), so we will examine that one.

OBJ files are simple enough that we can develop a basic importer relatively easily. In an OBJ file, lines of text specify vertex geometric data, texture coordinates, normals, and other information. It has some limitations—for example, OBJ files have no way of specifying model animation.

Lines in an OBJ file start with a character tag indicating what kind of data is on that line. Some common tags include

+   - v – geometric (vertex location) data
+   - vt – texture coordinates