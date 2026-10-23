So far, we have declared the constructors, destructor, and assignment operator and defined a function that reads a particular vertex in the finite element. Next, we define functions that manipulate the "index" field in the individual vertices in the finite element:

```
void resetIndices(){
    for(int i=0; i<N; i++)
        vertex[i]->setIndex(-1);
} // reset indices to -1
```

The "resetIndices" function in the above code resets all the indices of the finite-element vertices back to their initial value -1. However, since the vertices are of class "node" whose "index" field is private, this change must be done through the "setIndex" function, which is declared public in the "node" class. The same is true for the "indexing" function that renumbers the indices of vertices in increasing order:

```
void indexing(int&count){
    for(int i=0; i<N; i++)
        if(vertex[i]->getIndex()<0)
            vertex[i]->setIndex(count++);
} // indexing the vertices
;
```

This concludes the block of the "finiteElement" class. Next, we define the constructors declared above:

```
template<class T, int N>
finiteElement<T,N>::finiteElement(
    node<T>&a, node<T>&b, node<T>&c){
    vertex[0]=a.noSharingElement() ? new node<T>(a) : &a;
    vertex[1]=b.noSharingElement() ? new node<T>(b) : &b;
    vertex[2]=c.noSharingElement() ? new node<T>(c) : &c;
    for(int i=0; i<N; i++)
        vertex[i]->moreSharingElements();
} // constructor

template<class T, int N>
finiteElement<T,N>::finiteElement(finiteElement<T,N>&e){
    for(int i=0; i<N; i++){
        vertex[i] = e.vertex[i];
        vertex[i]->moreSharingElements();
    }
} // copy constructor
```

Next, we define the assignment operator declared above:

```
template<class T, int N>
const finiteElement<T,N>&
finiteElement<T,N>::operator=(finiteElement<T,N>&e){
    if(this != &e){
```