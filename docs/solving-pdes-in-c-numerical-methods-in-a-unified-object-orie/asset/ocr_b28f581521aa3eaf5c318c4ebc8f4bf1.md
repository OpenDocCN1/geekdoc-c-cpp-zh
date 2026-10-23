the boundary, with their vertices on the boundary. Each of these boundary triangles serves as the face of one tetrahedron only.

Once a boundary edge is divided in the refinement step, it makes sense to issue a normal vector from its midpoint towards the boundary. In fact, this normal vector points in between the two boundary triangles and meets the boundary at a new boundary point. By connecting this new point to the endpoints and midpoint of the original boundary edge and to the extra vertices of the boundary triangles, we obtain four new tetrahedra that lie next to the boundary and can be added to the original mesh to better approximate the boundary.

This way, the refinement step serves not only to divide the inner tetrahedra to refine the original mesh but also to improve the original mesh at the boundary. This automatic boundary refinement is implemented below.

First, let us implement a member function that takes the four corners "nI", "nJ", "nK", and "nL" of some tetrahedron in the mesh, and finds a neighbor tetrahedron that also shares the triangle vertexed at "nI", "nJ", and "nK" as a joint face. If such a neighbor tetrahedron indeed exists, then the function returns a reference to that corner. If, on the other hand, there is no such neighbor tetrahedron, then the above triangle must be a boundary triangle. In this case, the function returns a reference to the third argument "nK". (This is why "nK" is passed and returned by nonconstant reference.)

```
template<>
node<point3>&
mesh<tetrahedron>::findNeighbor(
        const node<point3>&nI,
        const node<point3>&nJ,
        const node<point3>&nK, const node<point3>&nL){
    for(mesh<tetrahedron>* runner = this; runner;
        runner=(mesh<tetrahedron>*)runner->next){
```

This is done in a loop over the tetrahedra in the mesh. The `<` operator is used to check whether each tetrahedron encountered in the loop indeed uses "nI", "nJ", and "nK" as its own corners. If it does, then its fourth corner is returned as output:

```
int nI = nI < (*runner)();
int nJ = nJ < (*runner)();
int nK = nK < (*runner)();
if(nI&&nJ&&nK&&!(nL<(*runner)())){
    nI--;
    nJ--;
    nK--;
    int nL = 0;
    while((nL==nI)||(nL==nJ)||(nL==nK))
        nL++;
    return runner->item(nL);
}
}
```

If, on the other hand, no such tetrahedron has been found, then "nK" is returned as output:

```
return nK;
}   //   find side-sharing tetrahedron
```