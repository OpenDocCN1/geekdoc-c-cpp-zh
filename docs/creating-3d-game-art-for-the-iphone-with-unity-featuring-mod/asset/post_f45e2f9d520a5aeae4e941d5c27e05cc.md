
There are other settings in the Import Assets that we'll discuss later. The Automatically calculate normals option and the Smoothing Angle parameter are very important at this stage in bringing our modo objects into Unity iOS as these settings directly affect your vertex count and we'll discuss this next.

## True Vertex Count

We've previously discussed how important vertex count is, so it's vital to note that you can't regard the vertex count in your 3D program as the true number of vertices in your object. In order to get the true vertex count for your mesh, you'll need to import your object into Unity iOS and check the Rendering Statistics window in the Game View as shown in Fig. 2.10. Be aware that Unity's Rendering Statistics window shows the resulting number of vertices sent to the GPU, which includes those added by lights and complex shaders.

![](img/d3e3fa4010906e98ec76be003a6e31c2_48_0.png)

There are several factors that cause the vertex count for your mesh to increase as it's rendered by the GPU. As a 3D artist creating game content, the concept that you can't trust the vertex count in your 3D application may seem foreign, but as you will see, you've already been dealing with these same factors in your everyday 3D work. Let's begin, by introducing the concept of triangle strips and degenerate triangles, which are the culprit behind our increased vertex count.

### Degenerate Triangles

Unity iOS tries to display your mesh as efficiently as possible using triangle strips. A triangle strip is a series of connecting triangles, sharing vertices as shown in Fig. 2.11. This allows for faster rendering and efficient memory usage.

![](img/d3e3fa4010906e98ec76be003a6e31c2_49_0.png)

**FIG 2.11** A Triangle Strip Is the Most Efficient Way of Describing a Mesh.

However, to effectively do this, Unity iOS must create what is called degenerate triangles or what is referred to as zero-angle triangles at points of various discontinuities such as mesh seams and UV borders. A degenerate triangle is formed by three collinear points or points that lay on the same line. It looks more like a line segment as shown in Fig. 2.12. The performance impact of these triangles can really add up on the GPU. In the next two subsections, we'll take an in-depth look at discontinuities that create degenerate triangles.

![](img/d3e3fa4010906e98ec76be003a6e31c2_49_1.png)

**FIG 2.12** A Degenerate Triangle Looks Like a Line Segment and Causes an Increased Vertex Count in Unity iOS.

### Smoothing Angles

In modo, you can adjust the smoothing of polygons on a per-material basis via the smoothing amount and angle. Without smoothing, the polygons that make up a mesh would be visible as facets. The Smoothing Angle is used to determine the maximum angle tolerance between connected polygons. If the angle between the connected polygons is greater than the Smoothing Angle setting, no smoothing will occur. The Automatically calculate normals toggle on the Import Assets dialog within Unity iOS is doing the same thing to smooth the mesh. By activating this toggle, you can then enter a smoothing angle just as you would in modo.

The issue of increasing vertex count comes into play when the GPU needs to render a hard edge. The hard edge occurs where connected polygons form at an angle that is greater than the smoothing angle. The GPU needs to split the vertices at this angle in order to create the hard edge, and this results in a mesh seam. Hard edges in your model are an area that you can begin to see an increase in vertex count. For example, on the left side of Fig. 2.13, you can see three connected polygons that have a smoothing angle of 180 degrees. On the right side, one of the polygons has been cut and pasted so that the vertices that connected it to the other polygons have been duplicated. You can now see that a hard edge has been created. This is similar to what is happening on the GPU when a hard edge in your object is encountered. The vertices at the hard edge need to be split to create the hard edge and thus cause the vertex count to increase.

### UV Seams

In the previous section, we talked about mesh seams. Now, we are going to look at the second half of this problem, which is UV borders or seams. When creating UVs for your objects, you need to minimize the amount of seams in your UV map. Just as we stated with mesh seams, when the GPU encounters a UV seam, the vertices are split.

![](img/d3e3fa4010906e98ec76be003a6e31c2_51_0.png)

**FIG 2.14** A Discontinuous UV Pair is Shown by the Blue-Highlighted Edges. The Blue Shading of the Edge Indicates the Vertices that Are Discontinuous.

This increases the number of vertices that need to be processed and the number of pixels that have to be drawn. Even when additional lights don't cause additional draw calls (for example, in VertexLit mode), they are still not free. For example, in VertexLit shaders, more lights equal the same number of draw calls and vertices to process, but each vertex has to do more computations. This makes it more expensive. Even in deferred rendering, assuming all objects are rendered in deferred, every light will increase the reported vertex count slightly because every light has some additional geometry to rasterize in order to run the lighting shader. For example, importing a single quad polygon and adding a light would double the vertex count from 4 to 8.

It's best to minimize the usage of lights in your scene or even better, not use them at all. Instead, it's a good idea to bake scene lighting into the diffuse texture map or use a lightmap and apply it with one of the iPhone lightmap shaders that ship with Unity.

In Chapter 8, "Creating Lightmaps Using Beast," we'll discuss the usage of lightmaps using Beast in Unity iOS.

## Modeling Tater and Thumper

In this section, we're going to take a look at how I created Tater and Thumper. We're going to discuss the important aspects of the process beginning with my workflow for creating objects for the iDevices. In Chapter 3, "Understanding Textures and UV Maps," we'll continue this discussion with a look at creating UV maps and texturing.

### My Workflow

I stated earlier that I wanted to keep the vertex count for Tater to less than 800 vertices. For Thumper, I wanted to keep its vertex count below 300 vertices. In the end, I was able to get Tater to 659 vertices and Thumper to 224 vertices. This gives me a combined count for the "hero" character and his weapon at 883 vertices. For this character, I didn't create a high-resolution mesh and then build a low-resolution version cage from it. This is a typical workflow in games as you can extrapolate a normal map from the high-resolution mesh. Instead, I went with a modified approach in that I began creating a low-resolution polygon cage and then optimized the mesh by adding geometry to areas of detail and reducing geometry once the base mesh was completed. As I worked on the base mesh, I used a combination of the Loop Slice and Edge Slice tools to quickly add and control edge loops on the mesh. I also tried to use quad polygons as much as possible and use triangles only in certain areas where I wanted to reduce geometry. For instance, in Fig. 2.15, I used a triangle in Tater's forearm to go from a higher resolution level around the bicep to a lower resolution level around the wrist.

![](img/d3e3fa4010906e98ec76be003a6e31c2_52_0.png)

**FIG 2.15** Here a Triangle Was Used to Reduce the Level of Detail from the Bicep to the Wrist.

When Unity iOS imports the FBX file, it will automatically be tripled, so there's no need to triple the polygons within modo.

### Creating Geometry

There aren't any special techniques to modeling for game objects for the iPhone and iPad when it comes to creating geometry. You'll quickly find that you'll be using all the common concepts for creating any model such as beveling, extruding, pushing and pulling points, and dividing and merging polygons. The skill in creating iOS content is in deciding where to add detail and where you can take it away while maintaining the overall shape of the model. You have to make calculated decisions on where you want to spend your vertices. Like I mentioned, I had a self-determined budget of less than 800 vertices for Tater and less than 300 vertices for Thumper, and the trick was in deciding where to spend my budgeted vertices.

Let's look at some examples of where I decided to place resolution in the Tater and Thumper game objects. In Fig. 2.16, you can see the resolution for Tater's head. I decided to add a small amount of detail to the face by having the mouth protrude from the face. I created an edge loop to outline the mouth. The mouth resolution is reduced at the corners of the mouth where the geometry is connected to the rest of the face. I also decided to extrude the nose from the face. Notice in Fig. 2.16 that the nose is very simple. There aren't any nostrils or much detail for that matter. It just roughly resembles a nose shape. The surface detail is created by means of the texture map as shown on the right. Also, in Fig. 2.16, you can see that the eye socket areas are simple flat polygons, and the eye resolution has been left to be totally defined in the texture map.

![](img/d3e3fa4010906e98ec76be003a6e31c2_53_0.png)

**FIG 2.16** In Order to Create a Low-Resolution Mesh, Detail Needs to Only Approximate the Shape of the Model. You Can Use Texture Maps to Further Accentuate Surface Detail.

In Fig. 2.17, you can see that the ammo barrel for Thumper, outlined in red, is intended to be round. However, I only used a six-sided disk, which was extruded and divided in the middle to maintain quad polygons. Although the ammo barrel is angular in nature, it approximates the rounded shape I was looking to create.
