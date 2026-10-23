# Chapter 13. Unstructured Finite-Element Meshes

After understanding the rules clearly, it is now time to break them. In fact, we do want the constructors to construct nothing but more references to existing nodes. Similarly, we want the destructor to destroy nothing but only reduce the number of these references. Therefore, the present constructors, destructor, and assignment operator should be written in an unusual way that violates the rule of thumb. The constructors and assignment operator operator should create no new nodes but merely new variables that contain the addresses of existing ones, thus providing more ways to access them. Similarly, the destructor should destroy no node that may still be used by some other finite element; it should only destroy the variable that contains its address, so it is no longer accessible through the destroyed finite element. Instead of actually removing the vertices, the destructor of the finite-element object only decreases their "sharingElements" fields to indicate that they are now being shared by fewer finite elements. Only those nodes whose "sharingElements" field is reduced to 0 are physically destroyed, because they belong to no finite element.

From the above discussion, it is clear that there is no point in deriving the finite element from the list of nodes. Indeed, in this case, most of the member functions in the "list" class in Chapter 3, Section 4 (including constructors, destructor, and assignment operator), would have to be overridden anyway along the above guidelines. Furthermore, in a list, the number of items is determined only in run time. This is unnecessary for a finite element, which always has a fixed number of vertices that never changes during the run. It makes more sense to define the finite element explicitly with no inheritance, with number of vertices 'N' that is fixed in compilation time:

```
```cpp
template<class T, int N> class finiteElement{
node<T>* vertex[N];
public:
finiteElement(){
for(int i=0; i<N; i++)
vertex[i] = new node<T>(0.,-1,1);
} // default constructor
finiteElement(node<T>&,node<T>&,node<T>&);
finiteElement(finiteElement<T,N>&);
const finiteElement<T,N>& operator=(finiteElement<T,N>&);
~finiteElement();
node<T>& operator()(int i){
return *(vertex[i]);
} // read/write ith vertex
const node<T>& operator[](int i)const{
return *(vertex[i]);
} // read only ith vertex
} // read only ith vertex
```
```

It is probably also possible to implement the finite element as an array of references-to-nodes rather than pointers-to-nodes. Still, we prefer the present implementation, to have a better understanding of the actual storage in the computer.