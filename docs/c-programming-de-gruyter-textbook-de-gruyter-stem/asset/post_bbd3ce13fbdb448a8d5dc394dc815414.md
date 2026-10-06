
## 6.3 Dynamic Memory Allocation — 235

This statement applies for memory space allocated to store T-type data, and uses values in the initialization list to initialize the data. If the application is successful, the new statement will return a T-type pointer to the starting address of the newly allocated memory space, and we can access the heap object using this pointer; if failed, the statement will return null pointer 0.

If the created heap object is a variable of a basic data type, the initialization of the variable is assigning values to the variable. For example,

```cpp
int *point;
point = new int(2);
```

The second statement dynamically allocates the memory space used to store int-type data and stores the initial value 2 into this space, and then it assigns the starting address to the pointer declared in the first statement.

If the created heap object is an object of a class, we need to call the constructor of the class according to the actual situations.

The delete operator is used to delete the heap object created by new, and release the memory space that the pointer points to. The format is

```cpp
delete pointer name;
```

If the deleted heap object is an object of a class, the destructor of the class will be called. Using an object created by new, we can only do the delete operation using delete. Using delete to release the same memory space repeatedly will lead to runtime errors.

Example 6.16: Create objects dynamically.cpp

```cpp
//6_16.cpp
#include<iostream>
using namespace std;
class Point {
public:
    Point()
    { X=Y=0; cout<<"Default Constructor called."<<endl; }
    Point(int xx, int yy)
    { X=xx; Y=yy; cout<< "Constructor called."<<endl; }
    ~Point()
    { cout<<"Destructor called."<<endl; }
    int getX() {return X; }
    int getY() {return Y; }
    void Move(int x, int y)
    { X=x; Y=y; }
private:
    int X,Y;
};
```

## 6 Arrays, Pointers, and Strings

```cpp
int main()
{
    cout<<"Step One:"<<endl;
    Point *Ptr1=new Point;
    //create object dynamically and initial value is not given,
    //so default constructor is called.
    delete Ptr1; //delete object, call destructor automatically
    cout<<"Step Two:"<<endl;
    Ptr1=new Point(1,2);
    //create object dynamically and initial value is given,
    //constructor with formal parameters is called
    delete Ptr1; //delete object, call destructor automatically
}
```

The running result of the program is as follows.

Step One:
Default Constructor called.
Destructor called.
Step Two:
Constructor called.
Destructor called.

The new operator can also create heap objects of the array type. In this case, we need to specify the array's structure. The syntax form of using the new operator to create a one-dimensional array is:

```cpp
new type name T[Subscript expression];
```

The subscript expression denotes the number of array elements. Initial values of array elements cannot be assigned during the memory allocation of array. Note that if the array is created by new, when it is deleted by delete, we should add "[]" before the pointer name.

## Example 6.17: Create an object array dynamically.

```cpp
//6_17.cpp
#include<iostream>
using namespace std;
class Point
{ //definition of the class is the same as in Example 6.16
    //....
}
```

## 6.3 Dynamic Memory Allocation — 237

```cpp
int main()
{
    Point *Ptr=new Point[2];   //create object array
    Ptr[0].Move(5,10);          //access members of array elements
                                     //pointers
    Ptr[1].Move(15,20);         //access members of array elements
                                     //pointers

    cout<<"Deleting..."<<endl;
    delete [] Ptr;               //delete the whole object array
}
```

The result is as follows:

- Default Constructor called.
Default Constructor called.
Deleting.
Destructor called.
Destructor called.

Here, we use dynamic memory allocation to realize dynamic creation of arrays. In this way the number of array elements can be determined according to the actual needs in runtime. The processes of creating and deleting arrays are somewhat tedious. A better way is to encapsulate the creating and deleting processes to construct a dynamic array class. Example 6.18 is a simple demonstration of a dynamic array class. A more complete dynamic security array will be introduced in Chapter 9.

**Example 6.18:** A dynamic array class.
The dynamic array class **ArrayPoints** created in this example uses a relationship with the Point class. Its UML figure is as shown in Figure 6.9.

| ArrayOfPoints |
| :--- |
| - numberOfPoints : int |
| + ArrayOfPoints(n : int) |
| ~ArrayOfPoints() |
| + Element(n : int) : Point& |

> Fig. 6.9: Relationship between the ArrayOfPoints class and the Point class.

![](img/5618306d085ac1bac8275d6c4c5bbf2a_254_0.png)

```cpp
//6_18.cpp
#include <iostream>
using namespace std;
```

## 6.3 Dynamic Memory Allocation — 238 — 6 Arrays, Pointers, and Strings

```cpp
class Point
{ //definition of the class is the same as in Example 6.16
    //....

class ArrayPoints
{
public:
  ArrayOfPoints(int n);
  ~ArrayOfPoints();
  Point& Element(int n);
private:
  Point *points;
  int numberOfPoints;
};
```

```cpp
int main()
{
  int number;
  cout<<"Enter the number of elements:";
  cin>>number;
  ArrayPoints arr(number);
  for(int i=0; i<number; i++)
  {
    arr.Element(i).Move(i*10, i*20);
    cout<<"Element " << i << ": X=" << arr.Element(i).getX() << ", Y=" << arr.Element(i).getY() << endl;
  }
}
```

*(Wait, the OCR text provided for the later pages was fragmented and repetitive. I will reconstruct the logic based on the provided raw OCR text while fixing the obvious errors and merging pages as requested.)*

## 6.3 Dynamic Memory Allocation — 239

The new operator can also create heap objects of the array type. In this case, we need to specify the array's structure. The syntax form of using the new operator to create a one-dimensional array is:

```cpp
new type name T[Subscript expression];
```

The subscript expression denotes the number of array elements. Initial values of array elements cannot be assigned during the memory allocation of array. Note that if the array is created by new, when it is deleted by delete, we should add "[]" before the pointer name.

will an error. This is because the new operation generates a pointer that points to a 25x10 two-dimensional array, but fp is a pointer of float type. For example,

```cpp
float *fp;
fp = new float[10];
```

The pointer cp can be used as a three-dimensional array. Please see the following program.

Example 6.19: Create multidimensional array dynamically.

```cpp
//6_19.cpp
#include<iostream>
using namespace std;
int main()
{
    float (*cp)[9][8];
    int i,j,k;
    cp = new float[8][9][8];
    for (i=0; i<8; i++)
        for (j=0; j<9; j++)
            for (k=0; k<8; k++)
                *(cp+i)+j)*k=i*100+j*10+k;
    delete [] cp;
}
```

## 6.3.2 Dynamic Memory Allocation and Release Functions

Besides using new and delete operators to dynamically manage memory spaces, C++ also inherits the dynamic storage management functions from C. Here we make a simple introduction:

- 1. Dynamic memory allocation function
Prototype: void *malloc( size size);
Parameter: size is the number of bytes to be allocated
Return value: return a pointer of void type if the allocation succeeds; otherwise null pointer
Header files: <stdlib.h> and <malloc.h>

- 2. Dynamic memory release function
Prototype: void free(void *memblock);
Parameter: memblock is a pointer that points to the memory space to be deleted
Return value: none
Header files: <stdlib.h> and <malloc.h>

## 6.4 Deep Copy and Shallow Copy

Although we introduced copy constructors in Chapter 4, for most of the simple examples we have encountered before, there is no need to write copy constructors, because default copy constructors can realize the copy of data elements between objects. There-
