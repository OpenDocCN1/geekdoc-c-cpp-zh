
![](img/7ba1225bb0e5a87be0fd35866408ffa7_97_0.png)

Figure 3.5: A small number of background threads continuously process the queue of regions that have been modified and regenerate the surface geometry. The main thread retrieves the results and uploads the geometry to the GPU.

A small number (1–4) of surface extraction threads run in the background and wait for the priority queue to contain task data to process. When a `TaskData` instance is available, a surface extraction thread will remove it from the priority queue and perform the Marching Cubes algorithm on its specified region. If other mesh processing tasks such as normal computation (Section 3.4) or splitting by material (Section 3.5.2) are necessary, then they are also performed by the surface extraction thread. The resulting vertex and index buffer pair is then assigned to the `TaskData` instance, which in turn is added to a queue of completed tasks.

The main thread is the only one that can copy the data to the GPU (at least on current generation hardware), and so this takes responsibility for removing items from the queue of completed tasks and uploading them to the graphics card. Semaphores are used to control access to the queues and to provide thread synchronization.

In order to give an indication of how well our threaded surface extractor performs, we ran each of our three test volumes through the surface extractor using between one and four threads. In each case, we measured the amount of time actually spent performing surface extraction. Time spent performing other tasks such as loading the volume from disk and uploading the meshes into GPU memory is omitted from these results, which can be seen in Table 3.2.

Table 3.2: Some typical timings for our threaded surface extractor quad-core 2.33 GHz CPU with 2 GB of memory.

| | No. of threads | Thread 1 time (ms) | Thread 2 time (ms) | Thread 3 time (ms) | Thread 4 time (ms) | Average time (ms) | Sum of times (ms) |
|---|---|---|---|---|---|---|---|---|
| Castle | 1 | 1094 | - | - | - | 1094 | 1094 |
| | 2 | 501 | 589 | - | - | 545 | 1090 |
| | 3 | 360 | 439 | 344 | - | 381 | 1143 |
| | 4 | 281 | 280 | 265 | 322 | 287 | 1148 |
| Mountain | 1 | 5292 | - | - | - | 5292 | 5292 |
| | 2 | 2717 | 2683 | - | - | 2700 | 5400 |
| | 3 | 1960 | 1888 | 1955 | - | 1912 | 5736 |
| | 4 | 1438 | 1340 | 1314 | 1518 | 1402 | 5610 |
| Earth | 1 | 9062 | - | - | - | 9062 | 9062 |
| | 2 | 4439 | 4455 | - | - | 4447 | 8894 |
| | 3 | 2926 | 3063 | 3045 | - | 3011 | 9034 |
| | 4 | 2549 | 2501 | 2510 | 2537 | 2524 | 10097 |

There are several things we can observe from this data. First, we can see that with several threads running the workload is split fairly evenly among them. A direct result of this is that the average time spent in a thread decreases as the number of threads increases. It's not quite a linear relationship, but it is pretty close, as shown by the "Average time" column. Second, we can see that the time to regenerate a region (64×64×64 in all these cases) is consistently around 20 ms. This means we would typically expect to pick up the results of modification 1–2 frames after it has occurred, and it makes 64×64×64 the largest region size we can practically use for real time modification. Lastly, we see that the time required to process a complete volume is typically just a few seconds.

## 3.5 Rendering

For the purpose of rendering, a bounding volume hierarchy is built with our region's geometry as the leaves. The bounding box of each piece of leaf geometry is at most the size of a region, but is usually smaller and it takes relatively little effort to trim the bounding box to the size of the actual mesh. Each internal node of the hierarchy is built from the eight nodes below it.

Because of the highly dynamic nature of our environments we do not perform any kind of precomputed visibility calculations. Visibility culling is currently handled simply by intersecting the view frustum with the bounding volume hierarchy, and rendering each piece of geometry whose bounding box is at least partly inside. This is a fast and efficient method for culling large amounts of geometry, but it is not an optimal solution for scenes with a high depth complexity. For these we are investigating the use of image-space methods such as Coherent Hierarchical Culling [4], but we do not yet know how well these will perform.

Lighting and shadowing algorithms are also fully dynamic, as the ability to modify the volume at any time makes the use of precomputed illumination very difficult. Normals for lighting are usually provided with the vertices (as discussed in Section 3.4.1), but in some cases it is possible to generate them on the fly. So far, we have applied only local illumination models, but some of the current research on real time global illumination may also be applicable. One of the many variants of the popular shadow mapping algorithm can be used to generate the real-time and dynamic shadows.

### 3.5.1 The Material System

When a surface is rendered, it is almost always desirable to provide additional surface detail to the object through the use of texture mapping. One of the key problems with generating geometry on the fly is that there is no opportunity for an artist to define the UV parameterization that specifies how these texture maps should be applied. Instead we need an automatic way of generating texture coordinates.

One of the most useful approaches (demonstrated in real time by Nvidia in their Cascades demo [3]) is known as *triplanar texturing*. This is performed in the fragment shader and uses blend weights derived from the surface normal to interpolate between three textures projected along the x, y, and z axes. That is, the first texture is sampled using the (y z) components of the fragment's world-space position and modulated by the x component of the normal, the second texture is sampled using the (x,z) components of the fragment's world-space position and modulated by the y component of the normal, and so forth. A fragment's world-space position can be determined by interpolating it from the vertices, and the components of a normal vector can be made to sum to one by squaring them. The snippet of Cg fragment shader code in Listing 3.1 demonstrates this process.

**Listing 3.1:** Triplanar texturing can project textures onto arbitrary geometry. This code receives textures, a normal, and a world position as input and computes the resulting color. Note that in order to preserve texture handedness, one of the UV coordinates must be negated whenever the dominant normal component is -x, +y, or -z. This is particularly important when working with normal maps but is not shown for simplicity.

```
// Interpolation means normals may not be unit length
normal = normalize(normal);

// Squaring a unit vector makes the components add
float3 blendWeights = abs(normal * normal);

// For each axis, sample the texture and multiply by
float4 colorMapValueYZ = tex2D(colorMapX, worldPos.
float4 colorMapValueXZ = tex2D(colorMapY, worldPos.
float4 colorMapValueXY = tex2D(colorMapZ, worldPos.
// Combine the results
float4 colorMapValue = colorMapValueXY + colorMapValueXZ;
...
```

Triplanar texturing works particularly well when applied to terrain, and when natural textures (rock, grass, etc.) are used. It does not respond particularly well to manmade textures containing sharp edges or other high frequency detail, as these do not blend well with each other. Variations on this idea are also possible, such as using six textures instead of three, or using one texture for all four lateral surfaces and different textures for the top and bottom.

An alternative method is to use the normal directly to lookup into a cube map texture. This is what was done for the surface of the Earth in Figure 3.1(b). In this case, the normals which were used for the lookup were generated on the fly by normalizing a vector from the center of the Earth to the vertex on the surface. This gave better results than using the normals generated by the methods in Section 3.4.

However, the conceptually simplest way to perform the parameterization is to use three-dimensional texture coordinates. In this case, the texture coordinates can be derived directly from the fragment's world-space position. Storing 3D textures on the GPU quickly becomes impractical because of their high memory requirements, but the 3D texture coordinates can easily be used as inputs into procedural texture generation routines. Referring again to Figure 3.1(b), the lava in the Earth's core is generated by using several octaves of Perlin noise running on the GPU [10].

Note that whichever technique is used to generate the texture coordinates, it is still possible to perform texture transformations by
