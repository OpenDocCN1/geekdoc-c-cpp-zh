At this stage, placing the element 90 in the new node does not satisfy max heap property. Hence, the new node needs to be moved up further. Here, 22 parents of the new node is smaller than 90 (the element to be inserted), slide 22 into the new node and the new node is moved up, which are shown by dashed lines (Figure 11.17(c)).

Now placing element 90 in the new node (Figure 11.17(c)) does not preserve the max heap property. Here, 85 parents of the new node are smaller than 90 (the element to be inserted), slide 85 into the new node and the new node is moved up as shown by the dashed line (Figure 11.17(d)).

Now placing element 90 in the new node (Figure 11.17(d)), preserves the max heap property. Since there are no nodes to be tested, element 90 in this location preserves the max heap property and it is the root node (Figure 11.17(e)).

C++ implementation of the method to insert an element into max heap is given in Figure 11.18.

```
Template<class T>
void MaxHeap<T>::insertEle(const T&x)
{
    if(full())
        throw OverFlow();
    //Move up
    int newnode=++cSize;
    for(;newnode>1&&x>array[newnode/2];newnode/=2)
        array[newnode]=array[newnode/2];
    array[newnode]=x; //element x inserted
}
```

Figure 11.18 Method to insert an element into max heap

# 11.3.5 Max Heap-Deletion

When the max element is deleted, an empty node is created at the root. Since the heap tree is now with one node less than the earlier number of nodes, the last element in the heap must move somewhere in the heap.

Deletion of max element 85 created an empty node as shown in Figure 11.19(b). The last element in the tree which is 6 should be moved somewhere into the tree. Moving 6 into proper location in the tree means ensuring max heap property after placing element 6 in its proper place.

Assume that the last element 6 is placed in an empty node. Now compare 6 with its children 22 and 40 (Figure 11.19(c)). If the parent is greater than or equal to both the children, then stop moving downwards. Otherwise, move down the empty node towards the larger child. In this case, it is moved towards the right. Hence, 40 is moved up by one level (Figure 11.19(c)).

Assume that element 6 is placed in an empty node (Figure 11.19(c)). In this position it does not maintain the max heap property. Now compare 6 with its children 26 and 35 (Figure 11.19(c)). Move down the empty node towards the larger child. The empty node is moved down towards the right (Figure 11.19(d)). This is the place for element 6 to be inserted. After inserting element 6 at this location, it maintains max heap property.

Max heap after inserting element 6 is shown in Figure 11.19(e).