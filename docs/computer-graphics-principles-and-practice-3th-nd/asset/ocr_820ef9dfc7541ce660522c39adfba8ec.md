```
```python
if (Din != Cin):  // crossed the line
    result.append(intersection(C, D, P, n))

if (Din): result.append(D)

return result
```
```

The algorithm produces some degenerate edges, which don’t matter for polygon rasterization but can cause problems when we apply the same ideas in other contexts.

# 36.5.2.2 Near-Plane Clipping

The 2D Sutherland-Hodgman algorithm generalizes to higher dimensions. To clip a polygon to a plane, we walk the edges finding intersections with the plane. We can do this for the whole view frustum, processing one plane at a time. Consider just the step of clipping to the near plane for now, however.

In camera space, the intersections between polygon edges and the near plane are easy to find because the near plane has a simple equation: z = −zn. In fact, this is exactly the same problem as clipping a polygon by a line, since we can project the problem orthogonally into either the xz- or yz-plane. We interpolate vertex attributes that vary linearly across the polygon linearly to the new vertices introduced by clipping, as if they were additional spatial dimensions. Listing 36.4 gives the details in pseudocode for clipping a polygon specified by its vertex list against the plane z = −zn, where zn < 0.

*Listing 36.4: Clipping of the polygon represented by the `vertex` array against the near plane z = −zn.*

```
```python
function clipPolygon(inVertices, zn):
    outVertices = []
    Let start = inputVertices.last()
    for end in inputVertices:
        if end.z <= zn:
            if start.z > zn:
                // We crossed into the frustum
                outVertices.append(clipLine(start, end, zn))

            // the endpoint of this edge is in the frustum
            outVertices.append(end)

        elif start.z <= zn:
            // We crossed out of the frustum
            outVertices.append(clipLine(start, end, zn))

        start = end

    return outVertices

function clipLine(start, end, zn):
    a = (zn - start.z) / (end.z - start.z)
    // This holds for any vertex properties that we
    // wish to linearly interpolate, not just position
    return start * a + end * (1 - a)
```
```