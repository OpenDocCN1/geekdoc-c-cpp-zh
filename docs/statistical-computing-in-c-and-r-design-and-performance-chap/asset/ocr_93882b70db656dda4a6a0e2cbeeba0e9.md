# ABSTRACT DATA STRUCTURES

```
#ifndef DARRAY_H
#define DARRAY_H

class dArray{
int* pA;
int Size, containerSize;
void pointerCheck(int* pa) const;
void resize();
void swap(int i, int j);

public:
    dArray() : pA(0), Size(0), containerSize(0){}
    dArray(int size, const int* pa);
    dArray(int size);

    dArray(const dArray& v);
    ~dArray();

    dArray& operator=(const dArray& v);
    int operator[](int k) const;

    void quickSort(int left, int right);
    void append(int value);
    void insert(int k, int value);
    int getSize() const { return Size; }
    int getContainerSize() const { return containerSize; }
};
#endif
```

The dArray class has three members: a pointer to int, pA, that holds the address of the beginning of a block of memory where the data in the dArray object is stored, a variable Size that gives the number of int objects that are currently held in storage, and containerSize which represents the total number of storage locations. Overloaded [] operator and two accessor functions provide access to these class members.

The constructors for class dArray need to allocate memory to hold the initial input data as well as some room for additional data that may arrive after the array's creation. There are various ways to accomplish this. A simple option might look something like

```
dArray(int size, const int* pa){
    Size = size;
containerSize = 2*Size;
pA = new int[containerSize];
pointerCheck(pA);
    for(int i = 0; i < Size; i++)
        pA[i] = pa[i];
}
```

The input to this constructor is a pointer to int and an integer value that gives the number of int objects that are stored (beginning) at the address held in the pointer. The value of size is used to initialize Size and pA after the information in pa is transferred to the pA class member. Although Size memory locations are needed to store the input data, memory is allocated for twice many, or containerSize, objects and the data is copied into the first Size of locations. Prior to copying the memory of allocation step for pA is checked using a variant of the pointerCheck function