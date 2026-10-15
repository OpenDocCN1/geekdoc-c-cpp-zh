# Algorithm 72: geomSewNGMap(gm, d, d', i): i-sew two darts for embedded n-Gmaps

Input: gm: an embedded n-Gmap; d, d' ∈ gm.Darts: two i-sewable darts; i ∈ {0, …, n}.

Result: i-sew darts d and d' by updating the embedding.

```
1 if i ≠ 0 then
2   it ← generic iterator(gm,d,(0, …, i − 2, i + 2, …, n));
3   it' ← generic iterator(gm,d',(0, …, i − 2, i + 2, …, n));
4   while it is not to its end do
5     if it' ∉ c0(it) then
6       deletePoint(it');
7     advance it to its next position;
8     advance it' to its next position;
9 sewNGMap(gm,i,d,d');
```

Thanks to the two marks, all operations are in constant time and no dart is processed twice.

This operation is illustrated in Fig. 7.6 by the 1-removal in an embedded 2-Gmap. The initial embedded 2-Gmap is given in Fig. 7.6(a) where the edge {3, 4, 5, 6} will be removed. Let us suppose that dart 3 is first processed. Then we iterate through all the darts in c0(3). Dart 6 is found which is linked with a geometrical point, thus e' is set to 6. Next dart 2 is found which does not belong to the removed edge thus todelete is set to false and d1 is set to 2. The vertex is not totally removed, and thus we only test if the dart linked with the geometrical point will be removed or not. Here dart 6 belongs to the removed edge, thus the embedding is updated by linking the geometrical point with dart 2. All darts in c0(3) are already considered thus they are no longer considered again in the first loop. Then dart 4 is found (for example); it belongs to the second vertex incident to the removed edge. We iterate through all the darts in this vertex {4,5}. Dart 4 is found. Since it is linked with a geometrical point, e' is set to 4, but the two darts belong to the removed edge thus todelete remains true. This means that the vertex will be removed during the combinatorial operation, and thus the associated geometrical point is deleted. The resulting embedded 2-Gmap is given in Fig. 7.6(b).

# 7.2.2.4 Geometrical Triangulation

A last example of operation for embedded n-Gmaps is the triangulation operation given in Algorithm 74. A new vertex is created, while there is no modification for existing vertices. Thus the additional geometrical layer consists only to create a new geometrical point and to associate it with the new vertex, denoted c0(d'). Since no point is associated with this new vertex when it is