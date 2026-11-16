
## 5.2 Let It Snow, Let It Snow, Let It Snow (and Rain)

The system is also more suited for games with relatively steady framerates. When the game framerate stutters drastically, the scrolling of the precipitation texture also stutters, which is more noticeable than the rest of the frame. In particular, the stretch emphasizes stutters, possibly causing the effect to appear to run backward.

Our technique has negligible impact on the game's overall framerate and has the same performance overhead for heavy precipitation as light precipitation, unlike a particle system. It ships with Microsoft Flight Simulator 2004: A Century of Flight, which maintains framerates of 15 to 60 fps across a range of consumer PCs.

## References

- [Langer03] Langer, Michael and Lingxiao Zhang. “Rendering Falling Snow Using an Inverse Fourier Transform.” SIGGRAPH Technical Sketch, 2003.

- [Reeves83] Reeves, William T. “Particle Systems—A Technique for Modeling a Class of Fuzzy Objects.” SIGGRAPH 1983, ACM. Detroit, Michigan.

## Widgets: Rendering Fast and Persistent Foliage

Martin Brownlow

martinbrownlow@msn.com

Games that render outdoor environments face a common problem: to look realistic, vast amounts of foliage must be drawn. For the purposes of this gem, foliage includes such features as plants, bushes, boulders, grass stalks, and other low-to-the-ground objects. These objects serve to obscure the ground textures in complex layers, lending a more realistic, voluminous appearance to the ground.

The objects used as foliage, which we shall refer to as *widgets*, are generally inert (they cannot be interacted with) and are there just to give the ground depth. Although these widgets could be randomly generated as new areas of the world are activated, an astute player might notice any differences when revisiting a previous location. Additionally, artists generally want control over everything that affects the look of their levels, and so prefer to define which types of foliage appear in which areas and how often they appear. In extreme cases, an artist might even want to go in and individually place several widgets to achieve a specific look.

Another consideration is that of destructibility: although widgets are essentially inert, it is often desirable to have world events affect them. For instance, if your game has huge explosions that change the underlying landscape textures to represent damage to the ground, it would be ridiculous for all the little tufts of grass to survive the blast unscathed. Some method of temporary or permanent removal of individual widgets or groups of widgets from the world will help the sense of immersion.

For efficient rendering of foliage, we need to address two distinct problems: we need to be able to quickly generate only those widgets that fall within the view frustum, and then to efficiently draw the resulting list of models.

### Meshes for Widgets

Although our intent is to render highly complex scenes covered with foliage, the individual meshes that make up the widgets need not be complex at all. In fact, the most effective models used as widgets generally use only a handful of double-sided polygons and a single texture. This simplicity allows us to render many more instances than we otherwise could, and so adds to the overall complexity of the scene. Figure 5.3.1 shows a simple example mesh that can be used as a widget, consisting of eight double-sided triangles and a texture map.

![](img/672fe9a2d008ba627b1991e15d70f43e_565_0.png)

FIGURE 5.3.1 A simple ground cover mesh.

Unfortunately, although the meshes themselves are simple, drawing them efficiently is not. Today's graphics hardware is designed to render huge amounts of triangles but performs best when rendering in blocks consisting of thousands of vertices. Rendering a thousand different copies of our eight triangle mesh is not going to be making the best use of graphics hardware.

### Drawing Widgets Efficiently

If we put aside for the moment the question of how to generate a list of the widgets that are to be drawn, we can look at how we are to efficiently draw a large number of tiny models. We have already determined that our widget meshes are to consist of a small amount of triangles and a single, simple material. We can further insist that each widget mesh should consist of exactly one triangle strip of indeterminate length.

To get the best throughput from our graphics hardware, we must submit as few batches of triangles to the hardware as possible, with each batch being as large as we can make it. This, then, is our objective: to find some way to batch together a large number of small models whose positions can change independently of one another from frame to frame (as the view changes, different sets of widgets will need to be drawn). This obviously rules out a large vertex buffer containing pretransformed widgets, since we would need to keep editing this buffer as the viewpoint moves around the world.

### Widget Batches

Although filling a vertex buffer with pretransformed widgets is out of the question, can we find a way to make the graphics hardware transform each widget by the correct matrix for us? In fact, we can; this is a similar problem to skinning, where each vertex indexes into a palette of matrices for its transform. By adding a matrix index to each vertex in the widget, we can make each widget index its own transformation matrix, then add multiple copies of the same widget to the buffer. Each individual widget must have the same index value for every vertex it contains, but consecutive widgets can and should have different values. Using an indexing system like this, we can place as many widgets in a single vertex buffer as there is room for matrices in the vertex constants. This method was employed by Gosselin, et al. for rendering large crowds of characters, but due to the skeletal animation, only four characters could be rendered in one API call [Gosselin04]. For foliage, we can render more widgets per API call. The following structure shows a possible vertex format for describing widgets:

```
typedef struct {
    float   position[3];
    float   uv[2];
    u32     mtlIndex;
} WIDGETVTX;
```

Now that we have created a vertex buffer containing several copies of the same widget, each with its own matrix index, we must figure out how to draw them in a single batch. We already know that each widget consists of a single triangle strip; we just need to stitch together the strips of consecutive widgets. This is done through the use of degenerate triangles; triangles that have two or more vertices that are coincident. To join two triangle strips together, we need to add four degenerate triangles, in the form of two indices. For example, to join the two strips, (1,2,3,4) and (8,9,10,11) we would repeat the last vertex of the first strip and the first vertex of the second strip to form the strip (1,2,3,4,4,8,8,9,10,11). In this example, our four degenerate triangles are (3,4,4), (4,4,8), (4,8,8), and (8,8,9). Each degenerate produces no pixels, and so the net result is the appearance of drawing two disconnected strips of triangles but with a single draw call.

However, joining strips in this fashion requires that the first strip be of an even number of indices. If the first strip is not an even number of indices in length, the winding order for the second strip will be wrong, since the winding order of the triangles in a strip is reversed for every other triangle. To get around this, if the first strip is an odd number of indices in length, we must first make it an even length by repeating the last vertex. For example, joining the two strips (1,2,3,4,5) and (8,9,10,11) results in a single strip of 12 vertices: (1,2,3,4,5,5,8,8,9,10,11).

Along with the vertex buffer containing multiple instances of a single widget, we must also create an index buffer containing a single strip to draw all these widgets. When creating this buffer, we must remember that the base vertex for each consecutive
