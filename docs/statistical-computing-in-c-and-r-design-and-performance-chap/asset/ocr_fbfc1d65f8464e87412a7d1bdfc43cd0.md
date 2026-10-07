# ADT PRIORITY QUEUE

```
int temp = A.PA[i]; A.PA[i] = A.PA[j]
A.PA[j] = temp;
}
void upHeapify(int i);
void downHeapify(int i, int size);
```

public:

```
Heap (int x) : A(DArray(1, &x)) {
const DArray& a;
void insert(const int& x);
int minimum() const {
return A.PA[0];
}
int& extractMin();
void heapSort();
void printHeap() const;
}
#endif
```

The class uses the array representation for a heap that was discussed in the previous section with the array storage being furnished by a DArray object. It is important for the Heap methods to be able to manipulate the objects in A as they must be reordered to preserve the heap property when elements are either added or extracted from the queue. An expedient to gain the access that is needed for such manipulations is to make Heap friend of DArray. This is accomplished by adding

+   friend class Heap;

to the DArray class declaration in Listing 9.1.
The Heap class constructor only initializes a Heap object. The actual process of building the heap is completed with the insert method. There are private methods swap, upHeapify and downHeapify that perform the re-arrangements of objects that are required for internal operations in a heap. These methods are used in the public methods extractMin and heapSort that remove the smallest value from the heap and sort the elements, in respect to extractMin, the minimum method simply returns the node at the top of the heap without removing. As a result, no rearrangement of the heap elements is necessary. There is also a utility printHeap that will print the contents of the heap to standard output.

void Heap::upHeapify(int i) {

```
int temp = i;
while (A.PA[(temp - 1)/2] > A.PA[temp]) {
swap(temp, (temp - 1)/2);
temp = (temp - 1)/2;
}

```

The main difference between the code and Algorithm 9.11 is the use of 0-offset indexing when accessing the elements of the array. Also, note that integer division automatically performs the floor operation in Algorithm 9.11.
The downHeapify method is slightly more complicated. Also, rather than giving a rote to implementation of Algorithm 9.12 we will allow downHeapify to only work on a portion of the tree. This feature will become useful in our heap code.