```
int k=0;
while((k==i) || (k==j))
    k++;
int l=0;
while((l==i) || (l==j) || (l==k))
    l++;
```

This way, we can define the subtetrahedra "t1" and "t2" that will be used later to replace the current tetrahedron:

```
tetrahedron t1(runner->item(i),itemij,
    runner->item(k),runner->item(l));
tetrahedron t2(runner->item(j),t1(l),
    runner->item(k),runner->item(l));
```

Furthermore, the edge midpoint "itemij" is also used in automatic boundary refinement. For this purpose, we must first check whether the edge that connects the corners indexed by 'i' and 'j' is indeed a boundary edge. This is verified by the local nodes "itemkb" and "itemlb" returned from inner calls to the "findBoundaryTriangle" function below. In fact, if these nodes indeed complete the original edge into boundary triangles, then this edge must indeed be a boundary edge:

```
node<point3>& itemkb =
    findBoundaryTriangle(
    runner->item[i],
    runner->item[j],runner->item(k),
    runner->item(l));
node<point3>& itemlb =
    findBoundaryTriangle(
    runner->item[i],
    runner->item[j],runner->item(l),
    runner->item(k));
if((&itemkb != &runner->item[l]) &&
    (&itemlb != &runner->item[k])) {
```

In this case, some straightforward geometry is used to define the normal vector "dirb" that is issued from the midpoint "itemij" and points in between the boundary triangles to meet the boundary at the new boundary point denoted by "boundaryCorner":

```
point3 edgeij =
    runner->item[i]() -
    runner->item[j]();
edgeij /= l2norm(edgeij);
point3 kMinusij =
    runner->item[k]() - itemij();
kMinusij -=
    kMinusij * edgeij * edgeij;
kMinusij /= l2norm(kMinusij);
point3 lMinusij =
```