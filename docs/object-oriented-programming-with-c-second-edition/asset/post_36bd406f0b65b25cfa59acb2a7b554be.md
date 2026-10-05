
## Operator Overloading, Type Conversion, New Style Casts, and RTTI 249

A* APtr = new A;

is translated by the compiler

```cpp
A* APtr = A::operator new(sizeof(A)); // nameless object-created
A::A(APtr); //constructor called for nameless object
```

While the statement

```cpp
delete APtr;
```

is translated by the compiler

```cpp
A::~A(APtr);//destructor called for nameless object
A::operator delete(APtr, sizeof(A)); // nameless object-destroyed
```

In order to understand the implications of these translations, let us consider a class that has a pointer as one of its data members. The class designer would certainly like to initialize this pointer to some valid value (NULL) in the constructor of the class.

```cpp
class String
{
    char * cStr;
public:
    String()
    {
        cStr = NULL;
        /*
        rest of the function String::String()
        */
        /*
        rest of the class String
        */
    }
}
```

However, if access is allowed to the private data members in the new operator function, the class designer might accidentally allocate some memory dynamically in the heap and 'cStr' point at it.

```cpp
void * String::operator new(const size_t size)
{
    cStr = new char
...
}
```

Now, when the constructor is called, a memory leak will occur because the value of 'cStr' will be straight nullified without first deallocating the memory block at which it is pointing. We may suggest the following improvisation (Listing 8.45) in the code for the class constructor:

- Listing 8.45 The new and delete operators are static

```cpp
A::A()
{
    if(cStr != NULL)
    {
        delete [] cStr;
        cStr = NULL;
    }
}
```

However, there is a serious drawback in this code above. It presupposes that if 'cStr' is not NULL, then it is definitely pointing at a dynamically allocated memory block that has been captured earlier by using the new operator. This is true only if the objects are created by the new operator. However, if objects are created in the normal fashion as:

- A A1;

then the mere fact that the code in the constructor of the class String finds that the value of 'cStr' is not NULL does not mean that 'cStr' is definitely pointing at a valid block of memory. In this fact, 'cStr' is simply a rogue pointer. Using the delete operator on such a rogue pointer will naturally lead to a run-time error. For reasons, the C++ compiler prevents access to the non-static data members of the class by treating the new operator and delete operator functions as static. We cannot force access to the non-static data members in the new and delete operator functions by avoiding the static keyword in their declarations.

It will not be of context to mention once again that the constructor does not actually 'construct' the object, it is merely a function that is called immediately after the memory for the object has been allocated. Its job is to ensure initialization of all data members to proper values and to acquire any resources if necessary. The destructor does not actually destroy the object in the sense that it does not actually deallocate the memory block by the object. It is merely a function that is called immediately before the memory is deallocated. Its job is to ensure a proper clean-up operation and to release all resources that were acquired during the lifetime of the object. The manner in which the compiler translates this to the new and delete operators makes this all clear. Moreover we may know how the global new and delete operators are called from the class member functions that overload them.

Values are passed to the constructor in the usual way even after the new operator is overloaded (Listing 8.46).

> Listing 8.46 Passing parameters to an overloaded new operator

```cpp
A * APtr = new A(10,20);
translated by the compiler as
A* APtr = A::operator new;
A::A(APtr,10,20);
```

We have already discussed, in an overall review for overloading the new and delete operators. The class designer overloads these operators if/she detects their default action inappropriate or inefficient for his/her class. Now, we will learn about the specific cases where overloading these operators becomes beneficial.

First let us see how the new operator works. In delete operator must know how much memory the new operator has allocated. The compilers solve this problem by prefixing the memory block allocated by the new operator. Therefore, as a result of the statement

## Operator Overloading, Type Conversion, New Style Casts, and RTTI

![](img/5bfa77b13fdaa376725789bb8c00ee79_264_0.png)

**Figure 8.2** Wastage of memory due to the default action of the new operator

- A* APtr = new A;

we get Part A and not Part B of Figure 8.2 (suppose objects of class A occupy 10 bytes)
This means every time the new operator is called for the class A, a separate block to store the memory of allocated will be allocated. This consumption of memory can be a real bottleneck in applications where memory is critical.

Before we come to a solution to this problem, we should know that even if the ‘new’ operator allocates array of objects, only one memory will be prefixed to the allocated memory block in order to hold its size. Therefore, the amount of extra memory allocated remains the same whether one object is created in the heap or an array of objects is created in the heap. The class designer can take advantage of this fact.

The class designer can ensure that when the new operator is called for the first time, a memory to hold a large number of objects gets allocated and the address of the memory block pool. The address returned will obviously be the address of the first object in the pool. Thereafter, every call to the new operator will return the address of the next available block from the pool.

This solution is explained in Figures 8.3 and 8.4. Suppose A is a class objects occupy 10 bytes. The class designer reckons that the pool will hold five objects at a time. Therefore, the pool size will be equal to 50 bytes. Let us consider the piece of code given in Listing 8.47.

- **Listing 8.47** Calling an overloaded new operator

```cpp
...
A* APtr1 = new A; //line 1
A* APtr2 = new A; //line 2
A* APtr3 = new A; //line 3
A* APtr4 = new A; //line 4
A* APtr5 = new A; //line 5
A* APtr6 = new A; //line 6
```

## 252 Object-Oriented Programming with C++

![](img/5bfa77b13fdaa376725789bb8c00ee79_265_0.png)

**Figure 8.3** Saving memory by overloading the new operator and modifying its behaviour

![](img/5bfa77b13fdaa376725789bb8c00ee79_265_1.png)

**Figure 8.4** Accessing the memory allocated by the overloaded new operator

A memory pool of 50 bytes (10 bytes for each of the five objects) will be created when line 1 executes (because the new operator is being called for the first time). When lines 2 to 5 execute, address of adjacent blocks are returned sequentially from this pool. After the first line executes, the following scenario emerges.

This process will continue until the sixth line is reached. After the fifth line execution, the memory pool will get exhausted. At this point of time, another memory pool of the same size (50 bytes—10 bytes each) will be allocated and the process repeat itself. All this is the effect of the class designer has written in the function that overflows the new operator.

The actual code is given in Listing 8.48.

- Listing 8.48 Overloading the new operator to improve efficiency

```cpp
/*Beginning of NewDeleteItemSave.h*/
#include<new.h>
class ClassNewDelete
{
    union {
        int x;
        ClassNewDelete * next;
    } static NO_OF_OBJECTS; static ClassNewDelete * head;
public:
    void setx(const int x = 0);
    int get() const;
    static void *operator new(const size_t);
};
/*End of NewDeleteItemSave.h*/
/*Beginning of NewDeleteItemSave.cpp*/
#include"NewDeleteItemSave.h"
int ClassNewDelete::NO_OF_OBJECTS = 5;
ClassNewDelete * ClassNewDelete::head;
int ClassNewDelete::get() const
{
    return v.x;
}
void setx(const int p)
{
    v.x=p;
}
void * ClassNewDelete::operator new(const size_t size)
{
    ClassNewDelete * temp,*p;
    temp = head;
if(!temp)
{
        temp = (ClassNewDelete*):operator new(sizeof(class ClassNewDelete)*NO_OF_OBJECTS);
        for(p=temp;p<=temp[NO_OF_OBJECTS-1];p++)
            p->v.next=p+1;
        p->v.next=0;
    }
    head=temp->v.next;
    return temp;
}
/*End of NewDeleteItemSave.cpp*/
```
