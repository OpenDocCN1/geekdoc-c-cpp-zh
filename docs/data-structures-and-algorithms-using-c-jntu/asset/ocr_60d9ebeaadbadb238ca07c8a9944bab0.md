![](bbox=[0.26, 0.08, 0.76, 0.31])

# (d) Element 16 inserted in the new node

# Figure 11.11 Insertion of an element

At this stage, placing 16 in the new node does not achieve min heap property. Hence, a new node needs to be moved up further. Since 23 parents of the new node is greater than 16 (the element to be inserted), slide 23 into the new node and the new node is moved up which is shown by the dashed line, (Figure 11.11(b)).

Now placing element 16 in the new node, shown by the dashed circle (Figure 11.11(b)), preserves the min heap property. A min heap is a complete binary tree in which the value in each node is less than or equal to those in its children (if any). Since the parent of 16 is less than or equal to 16, hence, it has reached its proper location. Element 16 in this location preserves the min heap property. Hence, element 16 is inserted in this location (Figure 11.11(d)). The C++ code for method insertEle is given in Figure 11.12(a).

Insert element x into min priority queue maintaining heap order.

```
```cpp
Template<class T>
void MinHeap<T>::insertEle(const T&x)
{
    // if (full())
    // throw Overflow();
    if(cSize==array.size()-1)
    array.resize(array.size()*2) ; //if the array is full,it is resized
    // Move up
    int newnode=++cSize;
    for(;newnode>1&&x<array[newnode/2];newnode/=2)
    array[newnode]=array[newnode/2] ;
    array[newnode]=x; //element x inserted
}
```
```

# (a) Method to insert an element into min heap