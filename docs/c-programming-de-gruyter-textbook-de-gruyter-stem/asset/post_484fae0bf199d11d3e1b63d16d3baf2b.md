
## 216 6 Arrays, Pointers, Strings

i pointed by i_pointer. Here, both the value of i and *i_pointer are 10. The former is direct access, and the latter is an indirect access by the pointer.
*i_pointer appears twice in the program, though its meanings are different. In the pointer declaration statement, before the identifier that declared the identifier is a pointer; in the output statement, ** is the pointer operator that leads an indirect access to the variable that the pointer points to.
Several points should be noted about the type of pointer.

- 1. We can declare a pointer to a constant. In this case, we cannot change the value of the object through the pointer, although the value of the pointer itself can be changed to point to other objects. For example,

```cpp
const char *name1= "John";//name1 is a pointer which points to a const
char s[]="abc";
name1=s;
//correct, the value of name1 can be changed
*name1='1';
//compile error, the value of the object that name1 points to
//cannot be changed through name1
```

Using a pointer that points to a constant can avoid the object from being changed accidentally. If we use a general pointer to store the starting address of a constant, the compiler cannot ensure that the object pointed by remains unchanged, and errors may occur during the running time. The following program segment is an example.

```cpp
char *name1 = "John";//name1 is a general pointer, but it stores the starting address
//of a string constant
*name1='A';
//compilation succeeds, but error in running. The content of the
//string constant cannot be changed.
```

Here, we try to change characters of the string constant "John" through pointer name1. Because name1 is a general pointer, the compiler is unaware of its error. But it goes wrong when running the program. In this situation, we should declare name1 as a pointer that points to a string constant.

- 2. We can declare a constant of the pointer type, and the value of the pointer cannot be changed during the execution of the program. For example,

```cpp
char *const name2 = "John";
name2="abc";
//error, name2 is a pointer constant, and its value cannot be changed//changed
```

- 3. In general, the value of a pointer can only be assigned to pointers of the same type. But there is a special kind of pointers that belong to the void type. Such a pointer can store the address of an object of any type. That is to say, pointers of any type can be assigned to a pointer variable of void type. Through type casting, we can access data of any type using a void-type pointer. Void-type pointers can also point to function except for the class member function.

**Example 6.6:** Using void-type pointers.

```cpp
void vobject;                      //Wrong, cannot declare a variable of void type
void *pv;                               //Right, can declare a pointer of void type
int *px; int i;
int main()                             //Functions of void type have no return value
{
    pv = &i;                            //Pointer of void type points to int variable
    px = (int *)pv; //type cast
    //assign the value of the pointer of void type to the pointer of
    int type
}
```

## 6.2 Pointers 217

### 6.2.5 Pointer Operations

A pointer is a data type. Like other data types, pointer variables can participate in some operations, including arithmetic operations, relational operations, and assignment operations. The assignment operation of pointers has been introduced before. In this section, we will introduce arithmetic operations and relational operations of pointers.

Pointers can perform simple addition and subtraction operations with integers. But the operational rule is special. When declaring a pointer variable, we must specify the type of the object it points to. Here, we will see that the results of addition and subtraction operations of pointers are closely related to the type of the pointer. If we have pointer p1 and integer n1, then p1+n1 denotes the address of the nith object after the current object p1 points to; p1-n1 denotes the address of the nth object before the current object p1 points to; "pointer++" or "pointer--" denotes the address of the next or previous object of the current object pointer points to. Figure 6.8 shows a simple diagram of the addition and subtraction operations of pointers.

Generally, arithmetic operations of pointers are associated with the use of arrays—for we can only get contiguous memory space when using arrays. If we perform arithmetic operations on a pointer that points to an individual variable and then we access the data through the result pointer, we may destroy the data or code of address. Therefore, when doing arithmetic operations of pointers, we must ensure that the result pointer points to an address that has been allocated in the program.

Relational operations of pointer variables refer to relational operations between pointers of the same type. If two pointers of the same type have the same value, it means that the two pointers point to the same address.

![](img/5618306d085ac1bac8275d6c4c5bbf2a_235_0.png)

**Fig. 6.8:** Arithmetic operations of pointers.

It is meaningful to do relational operations between pointers of different types or between pointers and nonzero integers. But pointer variables can be compared with the integer 0. This is a special mark of a pointer operation, which we will use in later examples.
The method of assigning pointers has been detailed in the last section. Here we stress that the value assigned to pointers must be address constants (e.g., array name) or address variables and they cannot be nonzero integers. If we assign 0 to a pointer variable, it denotes that this pointer is a null pointer that doesn't point to any address. For example:

```cpp
int *px; //declare a pointer p of int type
p=0; //set p as null pointer which doesn't point to any address
```

Why do we need to set a pointer as null using the method above? This is because sometimes when declaring a pointer, there is no definite address value that can be assigned to it. Only when the program runs to a point it assigns an address value to this pointer. During the period from the birth of the pointer to the time it has a definite value, its value is random. If we wrongly use this random value as an address to access some memory location, it will lead to unexpected error. Therefore, in this situation we should first set the pointer as a null pointer.

## 6.2.6 Using Pointers to Process Array Elements

The addition and subtraction characteristics of pointers make them especially suitable for processing the same type of data that is stored in a continuous memory space. An array is a set of same-type variables that have some ordinal relation; array elements are stored continuously; the array name is the starting address of the array. We can use pointers to do convenient and quick operations on arrays and array elements. For example,

```cpp
int array[5];
```

declares a one-dimensional array that stores five int-type elements. The array name is the starting address of the array (the address of its first element). That is, array is the same as &array[0]. Five integers in the array are stored orderly, so we can access array elements by using the array name and some arithmetic operations. The array element whose address is i (*array+i). For example, *array is array[0], and *(array+3) is array[3].

**Example 6.7:** Suppose there is an array a of the int type, which has 10 elements. Use three methods to output all the elements.

Program 1: Using array name and subscripts

```cpp
//6_7_1.cpp
#include <iostream>
using namespace std;
int main() {
    int a[10]={1,2,3,4,5,6,7,8,9,0};
    int i;
    for(i=0; i<10; i++)
        cout<<a[i]<<" ";
    cout<<endl;
}
```

Program 2: Using array name and pointer operations

```cpp
//6_7_2.cpp
#include <iostream>
using namespace std;
int main() {
    int a[10]={1,2,3,4,5,6,7,8,9,0};
    int i;
    for(i=0; i<10; i++)
        cout<<*(a+i)<<" ";
}
```
