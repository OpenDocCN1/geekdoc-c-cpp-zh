Let’s add the following command in `display()`, right before the `glDrawArrays()` call:

```
glPointSize(30.0f);
```

Now, when the rasterizer receives the vertex from the vertex shader, it will set pixel color values that form a point having a size of 30 pixels. The resulting output is shown in Figure 2.5.

![](bbox=[0.497, 0.11, 0.857, 0.302])

Figure 2.5
Changing glPointSize.

Let’s now continue examining the remainder of the OpenGL pipeline.

# 2.1.3 Tessellation

We cover tessellation in Chapter 12. The programmable tessellation stage is one of the most recent additions to OpenGL (in version 4.0). It provides a tessellator that can generate a large number of triangles, typically as a grid, and also some tools to manipulate those triangles in a variety of ways. For example, the programmer might manipulate a tessellated grid of triangles as shown in Figure 2.6.

Tessellation is useful when a lot of vertices are needed on what is otherwise a simple shape, such as on a square area or curved surface. It is also very useful for generating complex terrain, as we will see later. In such instances, it is sometimes

![](bbox=[0.176, 0.687, 0.824, 0.879])

Figure 2.6
Grid produced by tessellator.