
```
template<class T>
mesh<T>* mesh<T>::nextMesh() {
    return (mesh<T>*) this->next;
} // implicit conversion of the inherited pointer "next"
```

in which the field "next" inherited from the base "linkedList" class is converted implicitly to a pointer-to-mesh in the "return" command. Still, here we prefer the explicit conversion, to make the user aware of the potential risk.

A similar loop is used to index the vertices of the triangles in the mesh. This is done by the "indexing()" member function of the "finiteElement" class, which indexes vertices whose "index" field has not yet been set and is still −1:

```
int count=0;
for (mesh<T>* runner = this;
    runner; runner=(mesh<T>*)runner->next)
    runner->item.indexing(count);
return count;
} // indexing the nodes in the mesh
```

The above function also has an output: it returns the number of nodes in the mesh. This information can be quite helpful. In addition, the indices assigned to the nodes in the above function are used to refer to the corresponding unknowns in the stiffness system.

Here is a simple application that constructs and prints a mesh of three triangles. Note that when the "print" function is called, the mesh is interpreted as a linked list, and the "print" function of Chapter 3, Section 3.6, is invoked:

```
int main() {
    node<point> a(point(1,1));
    node<point> b(point(2,2));
    node<point> c(point(2,0));
    node<point> d(point(3,1));
    node<point> e(point(3,3));
    triangle t1(a,b,c);
    triangle t2(t1(1),t1(2),d);
    triangle t3(t2(0),t2(2),e);
```

Now, we have constructed the three required triangles. Note that, once a node is placed in a triangle, it is referred to as a vertex of this triangle rather than by its original name. This way, when an existing vertex of some triangle is also used as a vertex in a new triangle, its "sharingElements" field increases to reflect the fact that it is now shared by more triangles.

Next, we use the above triangles to form the required mesh:

```
mesh<triangle> m(t1);
m.append(t2);
m.append(t3);
t1.~triangle();
t2.~triangle();
t3.~triangle();
```

```
m.indexing();
print(m);
return 0;
}
```

## 13.5 Assembling the Stiffness Matrix

We are now ready to construct the stiffness matrix, as in Chapter 12, Section 5. Thanks to the above classes, the implementation is straightforward and transparent. Constructing the stiffness matrix is also called assembling, because the contributions from the different triangles in the mesh are assembled to form the required matrix elements.

The assembling is done by scanning the triangles in the mesh. When a triangle e with vertices i, j, and k as in Figure 12.1 is encountered, the corresponding elements A_i,j, A_j,k, and A_i,k in the stiffness matrix are incremented by the corresponding contribution from the integral over e, calculated as in Chapter 12, Section 5.

The loop that scans the triangles in the mesh uses a pointer-to-mesh variable named "runner". Since the "mesh" class is derived from the "linkedList" class, it would seem that "runner" can jump from item to item in it simply by writing "runner = runner->next". However, since the "next" field in the base "linkedList" class is of type pointer-to-linkedList rather than pointer-to-mesh, it must be converted to pointer-to-mesh before its value can be assigned to "runner". This conversion is done explicitly by adding the prefix "(mesh *)" just before the "next" variable. This conversion returns the address in "next" interpreted as the address of the "mesh" object rather than merely the address of the "linkedList" object.

Usually, this conversion is considered as risky, because in theory "next" can point to an object of class "linkedList" or any other class derived from it, with completely different member functions that could produce the wrong results. Fortunately, here the "next" field belongs to a "mesh" object and, therefore, must also point to a "mesh" object, so no risk is taken.

For each triangle scanned in the above loop, those elements in the stiffness matrix that couple vertices in it are incremented. In order to increment the correct matrix elements, the "index" field in these vertices must be used. This field contains the index of the vertex in the vector of unknowns x in the stiffness system.

Although the "index" field is private in the "node" class in Section 13.2, it can still be read as follows. Assume that we are at the middle of the loop, when "runner" points to the partial mesh consisting of the remaining triangles that have not yet been scanned. This partial mesh is then accessed simply by writing "*runner". Then, the "operator()" of the base "linkedList" class is invoked to access the first item in it simply by writing "(*runner)()". Then, the "operator[]" of the "finiteElement" class is invoked to read the i'th vertex in the triangle by writing "(*runner())[i]". Finally, the "getIndex" function of the "node" class is invoked to get the required index of the i'th vertex. This index is denoted by the capital letter 'I' in the code below.

The assembling code is of a rather high level, as it implements the mathematical definition of the stiffness matrix. Therefore, we may assume that some helpful low-level objects are available, although they have not yet been actually implemented. In particular, we assume that a class "stiffnessMatrix" is available, with an "operator()" that returns a nonconstant reference to the specified matrix element. In other words, if 'A' is a "stiffnessMatrix" object, then "A(I,J)" refers to the "(I,J)"th element in it. These assumptions are

sufficient for now; later on, the imaginary object "stiffnessMatrix" will be replaced by a more suitable object to store the stiffness matrix (Chapter 16, Section 5).

For simplicity, we consider only the case with constant diffusion coefficients P ≡ Q ≡ 1 (the Poisson equation). As discussed in Chapter 12, Section 5, the contribution to the stiffness matrix from the triangle e is based on integration over the reference triangle r in Figure 12.2. The integrand is the gradient of a nodal function in r times Sₑ⁻¹ times Sₑ⁻ᵗ times the gradient of a nodal function in r. The gradients of these nodal functions (φ₀,₀, φ₁,₀, and φ₀,₁) are stored in the three "point" objects "gradient[0]", "gradient[1]", and "gradient[2]", respectively:

```
point gradient[3];
gradient[0] = point(-1,-1);
gradient[1] = point(1,0);
gradient[2] = point(0,1);
```

The 2 × 2 matrix Sₑ in Chapter 12, Section 5, is stored in a "matrix2" object named 'S'. The first column in 'S' should be i − k in Figure 12.1, and the second column should be j − k. In order to define these columns correctly, one must have access to the geometric location of the vertices in the Cartesian plane. This information is obtained as follows: "runner" points initially to the entire mesh and is then advanced gradually to point to subsequent submeshes that contain fewer and fewer triangles. In other words, "*runner" is the linked list whose first item is the current triangle under consideration. Using the "operator()" of the base "linkedList" class, this triangle is obtained as "(*runner)()". Now, by applying "operator[]" in the "finiteElement" class, the i'th vertex in this triangle is obtained as "(*runner)()[i]". Finally, by applying the "operator()" of the "node" class, the required location of this vertex in the Cartesian plane is obtained as "(*runner)()[i]()". The matrix 'S' is thus defined as follows:

```
for(const mesh<triangle>* runner = &m; runner;
    runner=(const mesh<triangle>*)runner->readNext()){
  matrix2 S(((*runner)()[1]() - (*runner)()[0](),
             (*runner)()[2]() - (*runner)()[0]()));
```

We are now ready to calculate the integrand as the gradient of a nodal function in r times Sₑ⁻¹ times Sₑ⁻ᵗ times the gradient of a nodal function in r. For this purpose, we use the "det()", "inverse()", and "transpose()" functions implemented at the end of Section A.5 of the Appendix:

```
matrix2 Sinverse = inverse(S);
matrix2 weight =
    abs(det(S)/2) * Sinverse * transpose(Sinverse);
```
