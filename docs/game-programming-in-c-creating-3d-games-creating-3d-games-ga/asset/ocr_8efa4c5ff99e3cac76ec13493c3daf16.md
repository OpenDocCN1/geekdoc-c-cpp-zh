```
foreach MeshComponent m in scene
    foreach Pixel p in m
        float depth = p.Depth()
        if zBuffer[p.x][p.y] < depth
            p.draw
        endif
    endfor
endfor
```

With z-buffering, drawing the scene in any arbitrary order will look correct if there are no objects with transparency. This is not to say that the order is irrelevant. For example, drawing a scene back-to-front yields the same amount of overdraw as the painter's algorithm. Conversely, drawing a scene front-to-back yields zero overdraw. But the gain of z-buffering is that any arbitrary order works. And because z-buffering is on a per-pixel basis, not a per-object or per-triangle basis, it will work even for the overlapping triangles in Figure 6.5.

Luckily, z-buffering is not something a graphics programmer implements anymore; you merely need to enable it. OpenGL supports depth buffering with minimal effort. (OpenGL uses the term depth buffer instead of z-buffer.) First, prior to creating the OpenGL context, you need to request a depth buffer (24-bit is a typical size):