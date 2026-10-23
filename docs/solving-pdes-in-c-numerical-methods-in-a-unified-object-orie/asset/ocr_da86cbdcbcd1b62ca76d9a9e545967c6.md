This function is now used to check whether the edge leading from "nI" to "nJ" is a boundary edge or not. For this purpose, it is sufficient to check whether the edge is surrounded by tetrahedra that use it as their joint edge. If it is, then it can’t be a boundary edge, as it is separated from the boundary by some tetrahedron in every direction. If, on the other hand, it isn’t, then it must be shared by two boundary triangles, so it must indeed be a boundary edge that lies next to the boundary.

The "findBoundaryTriangle" function below considers a particular tetrahedron that indeed uses the edge leading from "nI" to "nJ" and also has two other corners, denoted by "nK" and "nL". By calling the above "findNeighbor" function, a neighbor tetrahedron that also uses the corners "nI", "nJ", and "nK" is found. The fourth corner of this tetrahedron, which is returned by the "findNeighbor" function, is then used to repeat the same process and to find yet another neighbor tetrahedron that shares a face with the first neighbor tetrahedron and also shares the original edge that leads from "nI" to "nJ".

This process is repeated again and again in a loop, finding more and more subsequent tetrahedra that share the original edge as their joint edge. In fact, the process can terminate in two possible ways only. If the original edge is not a boundary edge, then the process continues throughout the tetrahedra that surround this edge, until the original node "nL" is reached from the other side. "nL" is then returned as output to indicate that the original edge is not a boundary edge. If, on the other hand, the original edge is indeed a boundary edge, then the process continues until a boundary triangle is reached. At this point, the process terminates, as there are no more neighbor tetrahedra. Thus, the function returns the third vertex of this boundary triangle, to indicate that the original edge is indeed a boundary edge.

```
template<
node<point3>&
mesh<tetrahedron>::findBoundaryTriangle(
    const node<point3>&nI,
    const node<point3>&nJ,
    node<point3>&nK, node<point3>&nL) {
node<point3>* nKrunner = &nK;
node<point3>* nLrunner = &nL;
```

Here "nKrunner" points to the so-called forward node (which is initially "nK"), and "nLrunner" points to the so-called backward node (which is initially "nL"). In the loop that follows, both "nKrunner" and "nLrunner" advance: "nKrunner" advances to point to the fourth corner of the next neighbor tetrahedron, and "nLrunner" takes the old value of "nKrunner":

```
while( (nKrunner != &nL) &&
    (nKrunner != nLrunner) ) {
    node<point3>* nKkeep = nKrunner;
    nKrunner =
    &findNeighbor(nI,nJ,
        *nKrunner,*nLrunner);
    nLrunner = nKkeep;
}
```

The loop can terminate in two possible ways. If "nKrunner" points at "nL", then the original edge that leads from "nI" to "nJ" must be surrounded by tetrahedra that share it as their joint