
One possible avenue of advancement is to create an algorithm to deterministically place foliage in a small area, and then create BSP trees for these areas as they approach the viewpoint. Such an algorithm would allow us to take advantage of the memory cache efficiency of the BSP tree while keeping actual memory usage to a minimum. This would give us the ability to populate worlds of increasing size with foliage for a constant memory cost, since only BSP trees that could possibly be rendered with the current viewpoint need to exist at any given time.

## References

[Gosselin04] Gosselin, David, Pedro V. Sander, and Jason L. Mitchell, “Drawing a Crowd: Instancing in Current Hardware.” In ShaderX³ (edited by Wolfgang Engel), Charles River Media, 2004.

## 2.5 Dimensional Impostors for Realistic Trees and Forests

Gábor Szíjártó, Technical University of Budapest
szijarto.gabor@freemail.hu

One of the major challenges in developing techniques for realistic and high-performance visualization of outdoor environments is the rendering of vegetation. Convincing modeling of trees and bushes requires a very large number of polygons that exceed the limits posed by the current rendering hardware. A number of methods have been proposed in the past to address the issue, most of which are variants of multiresolution modeling and level-of-detail algorithms.

In this gem, a 2.5 dimension impostor based method [Szijarto03] is developed for high-resolution tree rendering, which uses the structure of conventional trees. Moreover, it takes advantage of the programmable rendering pipelines available on the recent video cards. The algorithm uses view-dependent 2.5 dimensional impostors to visualize convincing trees in most levels of detail. Due to the use of impostors, the performance depends heavily on the fill rate of the video card.

### Introduction

It is often useful to define specific scales of simulation at which a vegetation-rendering algorithm should provide the required level of realism. Most applications can be assigned to one or more of the following categories:

- Insect scale: The level of simulation where a consistent, realistic depiction of individual branches and leaves is expected. (The avatar can climb the tree.)
- Human scale: Scenes must look realistic at distances ranging from an arm’s reach to some tens of meters away. Consistency is desired but not required. (The avatar can bump into trees, even dash through bushes, but does not focus on specific details.)
- Vehicle scale: At this level, vegetation serves as little more than a backdrop. Individual trees are almost never focused upon, and consistency is not required. Viewing distance may exceed several hundred meters. (The avatar is usually moving through the environment at some altitude above the ground at faster than running speeds.)

The focus of this research has been an algorithm for human and vehicle scale simulation, with possible application in low-altitude (helicopter and glider) flight, land vehicle simulators, and first person shooters.

Vegetation visualization seems to be a hard nut to crack. There are two general approaches: geometry- and image-based methods. As its name suggests, techniques of the former group use geometric representations of the foliage. As it takes roughly one hundred thousand triangles to build a convincing model of a single tree, some form of Level of Detail (LoD) rendering technique must be applied to reduce the polygon count for a given frame to a reasonable level [Remoran03], [Pupp97]. Visually pleasing results can only be achieved with complex algorithms or significant memory overheads. At this point in time, geometry-based methods are not acceptable for real-time applications. Image-based methods represent a trade-off of consistency and physical precision in favor of more photorealistic visuals.

### Previous Image-Based Methods

The simplest of all image-based methods is sprite rendering, shown in Figures 5.4.1 and 5.4.2. This technique is analogous to using a cardboard cut-out with a tree-like image painted on it that always faces the camera. Though the resulting visuals are far from satisfactory, the technique is often used to depict smaller plants.

![](img/672fe9a2d008ba627b1991e15d70f43e_577_0.png)

FIGURE 5.4.1 Sprite rendering. The textured polygon is always facing the camera.

![](img/672fe9a2d008ba627b1991e15d70f43e_578_0.png)

FIGURE 5.4.2 Billboard with arbitrary position and orientation.

Two obvious improvements introducing some form of view dependence are sets of view-dependent sprites and more complex cutouts. The view-dependent sprite method simply regenerates a finite set (usually 4 or 8) of views and, at runtime, presents the one closest in alignment with the viewing direction. A popping artifact is visible when there is an alignment change and another view is selected. The complex cutout approach uses texture transparency and blending to render more than one view at the same time onto properly aligned surfaces, as shown in Figure 5.4.3. Both methods yield surprisingly acceptable results in vehicle scale simulations but fail to deliver quality in close-up views. It is also not trivial to introduce varying shapes and sizes of trees without overtaxing memory. Lighting is also a concern with this method.

One of the most advanced methods actually implemented in commercial entertainment software is the basic freeform textured tree model with some LoD applied, as shown in Figure 5.4.4. Though the idea is quite straightforward, only in the last few years has hardware become powerful enough to handle the task. Resulting visuals are satisfactory, although, due to the simple geometric model used, close-up views usually look artificial and variations are usually introduced through new models or through combining model parts. Increasing the number of trees in a scene quickly reduces performance. Most recent hardware scale simulators rely on this technique, and on the raw hardware power to cope with it.

![](img/672fe9a2d008ba627b1991e15d70f43e_579_0.png)

![](img/672fe9a2d008ba627b1991e15d70f43e_579_1.png)

### Improving on Previous Methods

The techniques described so far all take advantage of the fact that it is much faster to render a recorded image of a tree than to actually process the geometric information describing the tree model. There are two key reasons for this:

- A leaf on a tree is usually mapped to only a few pixels. On today's hardware, rendering a pixel is much faster than transforming a triangle.
- The number of obscured leaves is very large. Thus, a significant number of transformations would be performed in vain.

Image-based methods suffer from two significant drawbacks: fixed perspective and invariance to motion and rotation. Fortunately, in tree rendering, the fixed perspective is not so disturbing. The tree canopy is a fairly irregular structure, and the human eye is far less sensitive to perspective distortions of irregular shapes than regular ones. The other problem is far more disturbing. Leaves are static as the camera moves, while it would be expected for some leaves to appear and others to become obscured as the viewer moves relative to the tree. This issue has to be addressed in some way to raise rendering quality to an acceptable level. Popping artifacts are about as disturbing to the human eye as static textures in motion. Thus, we can conclude that to achieve convincing visuals, the geometry of leaves has to be processed to some extent.

The algorithm described in the following sections renders the tree canopy as a collection of small leaf clouds. A leaf cloud consists of only a fraction of the total leaves needed to model the entire tree. The amount of geometry needed to render a leaf cloud is small enough to handle on a per-frame basis. The idea is to process a leaf cloud, render it to a texture, and apply that texture multiple times to render the tree canopy, thus introducing the motion parallax missing from previous image-based methods. However, because the leaf cloud textures overlap, artifacts will occur unless depth information is handled correctly. Introducing depth-consistent impostor rendering results in images where leaf clouds can correctly overlap with other leaf clouds, branch geometry, other trees, or any other object in the scene.

### The Algorithm

The proposed technique is an improvement to traditional impostor rendering. Impostor rendering has two stages. The first stage is a view-dependent render-to-texture operation (drawing the impostor), the result of which is used in the second stage usually as sprite or billboard texture (see Figures 5.4 and 5.4.6).

The idea is to represent the tree canopy with more than one sprite, as shown in Figure 5.4.5. Sufficient variations can be introduced by the perturbation of the relative positions of the sprites in space. Rendering two or three different textures for sprites can introduce even more diversity. Individual sprites can also be blended using different colors, again to introduce variations, and even lighting. A canopy depicted using 10 to 100 sprites can look very convincing in still images, as shown in Figure 5.4.8, even if the same texture is repeated over all sprites.

However, the view independence of sprites makes the previous method quite useless for real-time rendering when the viewer is in motion. As sprites are always facing the camera, if their appearance is constant, they upset the motion parallax, producing very unrealistic results. The introduction of view dependence through the use of
