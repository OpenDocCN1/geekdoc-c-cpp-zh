```
// zBuffer[x] [y] grabs depth at that pixel
foreach MeshComponent m in scene
    foreach Pixel p in m
        float depth = p.Depth()
        if zBuffer[p.x][p.y] < depth
            p.draw
        endif
    endfor
endfor
```