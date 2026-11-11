triangle strips [EMX02] is common since many hardware pipelines are highly optimized for that succinct encoding type.

**Simplification** is a form of compression similar to the image compression of JPEG or audio compression of MP3. The compression is **lossy** in that the resultant geometry is not as accurate as the original. But just as MP3 compression produces music files that are “good enough” for many purposes, geometric simplification also can be tuned to be satisfactory for specific applications.

For example, if an object or the viewpoint is in motion, it may be possible to simplify the object without the viewer being aware. Or, if the object’s “importance” (measured in terms of how many pixels its projected image takes up on the viewport) is lower than some threshold, a certain amount of simplification may be possible without damage to the object’s legibility.

There are numerous types of geometric simplification, including the following.

+   - **Continuous Level of Detail/Multiresolution Geometry/Geomorphing/Selective Refinement/Progressive Meshes/Hierarchical Dynamic Simplification**

A number of algorithms, known by a variety of names, can be used for automatic simplification of a mesh in a manner that fine-tunes the amount of simplification based on the importance (as described above) of the object’s image. These algorithms vary widely in their strategies and usage scenarios, and they should be studied by any developer needing “just enough but not too much” simplification.

As an example, a progressive mesh (described in detail in Section 25.4.1) provides for storage of a mesh at many resolutions in a single data structure. The structure can be thought of as a sequence: The coarsest (least-expensive, lowest-quality) mesh is stored as the “core,” followed by a sequence of “reconstruction records” describing how to incrementally restore the higher-resolution information. The renderer of this mesh sequence can choose to stop reconstruction at any point in the sequence; the more the processor continues to execute the reconstruction records, the closer the resultant mesh is to the original resolution.

Note that opportunities for implementation of some of these algorithms lie both in the AMIP and directly on the graphics hardware.

+   - **Discrete Level of Detail**

When the application needs full control over the simplified geometry, this technique can be used instead of fully automated mesh simplification. Key objects are specified via multiple mesh definitions (e.g., high-, medium-, and low-detail versions), and the application uses the one appropriate for the object’s current importance (as described above).

+   - **Simulating Complex Geometry**

For certain applications (e.g., the bumpy surface of an orange, or rocky terrain seen from afar), instead of representing the geometry in the actual mesh and bearing the cost of lighting/shading calculation, an application can use tricks to fool the eye into seeing complex geometry that is not actually part of the mesh. Texture mapping, as described in Section 1.6.1, is a primitive technique that wraps the mesh with an image in order to provide color and translucency variation. More sophisticated algorithms, described in Chapter 20, include normal mapping, displacement mapping, bump mapping, and procedural texturing. As an extreme case of cost reduction,