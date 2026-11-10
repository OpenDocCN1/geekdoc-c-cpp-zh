texture coordinates so as to draw our bricks onto the pyramid. One simple (albeit imperfect) way would be to make the top center of the image correspond to the peak of the pyramid, as follows:

![](bbox=[0.329, 0.201, 0.67, 0.317])

We can do this for all four of the triangle sides. We also need to paint the bottom square of the pyramid, which comprises two triangles. A simple and reasonable approach would be to texture it with the entire area from the picture (the pyramid has been tipped back and is sitting on its side):

![](bbox=[0.26, 0.452, 0.73, 0.583])

Using this very simple strategy for the first nine of the pyramid vertices from Program 4.3, the corresponding set of vertices and texture coordinates is shown in Figure 5.3.

```
```
        vertices                texture coordinates
   (-1.0,-1.0, 1.0)              (0, 0)      // front face
   ( 1.0,-1.0, 1.0)              (1, 0)
   ( 0, 1.0, 0)                  (.5, 1)

   ( 1.0,-1.0, 1.0)              (0, 0)      // right face
   ( 1.0,-1.0,-1.0)              (1, 0)
   ( 0, 1.0, 0)                  (.5, 1)

   ( 1.0,-1.0,-1.0)              (0, 0)      // back face
   (-1.0,-1.0,-1.0)              (1, 0)
   ( 0, 1.0, 0)                  (.5, 1)
   etc.
```
```

**Figure 5.3**
Texture coordinates for the pyramid (partial list).