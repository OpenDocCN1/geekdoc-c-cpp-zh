
## 6.1.1 Declaration and Use of Arrays

### 1. Declaration of Arrays

An array is a user-defined data type, and needs to be declared before being used. The declaration of an array should consist of the following parts:

- a) Define the array's name;
- b) Define the types of its elements;
- c) Define the structure of the array (such as the dimension of the array, the size of each dimension, and so on)

The common form for declaring an array is as follows,

```
Data type Identifier[Constant expression 1]
[ Constant expression 1]...;
```

The type of elements in an array is specified by "Data type". This data type can be either basic types such as int, float, or user-defined types such as structure and class.
The array name is specified as the "Identifier". **The array name is a constant, which represents the starting address of array elements in memory.**

Expressions like "Constant Expression 1", "Constant Expression 2", etc. are called subscript expressions. They must be of the unsigned int type. The subscripts of an array are used to limit the number of elements in an array, and also to specify the order and position of each element in the array. In C, a n-dimensional array, whose elements is actually an (n-1)-dimensional array. Thus, in C n-dimensional array is declared as the array name plus subscript expressions, where the value of each subscript expression denotes the size of each dimension (note that this is not the upper bound of the subscript in that dimension). The number of array elements can be calculated by multiplying the values of all subscript expressions from the array declaration. For example,

```
int b[10];
```

indicates that b is an array of the int type, and it has 10 elements: b[0]...b[9]. It can be used to store an integer array of 10 elements.

```
int a[5][3];
```

indicates that a is a two-dimensional array of the int type. The size of its first dimension is 5 (subscripts from 0 to 4), and the size of its second dimension is 3 (subscripts from 0 to 2). Thus the total number of a's elements is 15. It can be used to store a table of int type, which has five rows and three columns. It is worth noting that the value of array subscripts is 0. For the array a declared above, the first element is a[0][0], and the last element is a[4][2]. In other words, the subscript of every dimension starts from 0.

### 2. Use of Arrays

When using an array, we can operate its elements respectively. Array elements are denoted by subscripts. To a declared array, we can reference its elements like this:

```
Array name[Subscript expression 1][Subscript expression 2] ... ;
```

Here the amount of subscript expressions depends on the dimensions of the array. For an N-dimensional array, each of its elements has to be denoted by N expressions.

Each element of an array equals a variable of the corresponding type. We can use array elements where the variable of that type is permitted. For example, we can use element of an integer array like an integer variable. Similarly, each element of an array of a class type can be used as a common object of that class.

- a) Subscript expression of array element can be any arithmetic expressions as long as the value of the expression is an integer.
- b) The subscript value of one dimension of an array element cannot exceed the upper and lower bounds of that dimension of the array originally declared. Otherwise, the “Array is out of range” error may occur when running.

Example 6.1: Declaration and Use of Arrays.

```cpp
//6_1.cpp
#include <iostream>
using namespace std;
int main()
{
    int A[10],B[10];
    int i;
    for(i=0;i<10;i++)
    {
        A[i]=i*2-1;
        B[10-i-1]=A[i];
    }
    for(i=0;i<10;i++)
    {
        cout<<"A["<<i<<"]="<<A[i];
        cout<<"B["<<i<<"]="<<B[i]<<endl;
    }
}
```

In this program, we declare two one-dimensional arrays A and B with 10 elements each. We use for loop to assign values to their elements. When referring to the elements of B, we use arithmetic expressions as subscripts. After running the program, 0, 1, ..., 9 are assigned to elements of A: A[0], A[1], ..., A[9] respectively. B's elements are A's in reversed order.

If we rewrite the two loop statements for (i=0; i<10; i++) and (i=1; i<=10), it won't produce any error in compiling process. In the running process, instead of getting correct results, we may encounter unexpected errors. This is a typical "array bound out of range" error.

### 6.1.2 Storage and Initialization of Arrays

#### 1. Storage of Arrays

Array elements are stored ordered continuously in memory. They occupy a group of consecutive locations in memory. Elements that are logically adjacent are physically adjacent. The array name represents the starting address of array elements. The elements of a one-dimensional array are simply ordered continuously according to their subscripts. Elements of multidimensional array are also ordered continuously, and the rule of storage order is very important. The issue of storage order of array elements is related to what kind of order we operate the array elements when processing the array as an entity. Many operations in C++ are related to array initialization and data transfer.

A one-dimensional array can be viewed as a column vector in mathematics, and each element is stored in memory according to their subscripts. For example the following array statement

```cpp
int ay[5];
```

declares a one-dimensional array of int with five elements. This array can be viewed as a column vector [ay[0], ay[1], ay[2], ay[3], ay[4]]. The storage order of array elements is demonstrated in Figure 6.1.

A two-dimensional array can be viewed as a matrix in mathematics; the first subscript of each array element is called the row subscript, and the second subscript is called the column subscript. For example the array statement

```cpp
int M[2][3];
```

declares a two-dimensional array, which equals a matrix with two rows and three columns:

```cpp
M = {{M[0][0], M[0][1], M[0][2]], [M[1][0], M[1][1], M[1][2]}};
```

| ay[0] | ay[1] | ay[2] | ay[3] | ay[4] |
| :--- | :--- | :--- | :--- | :--- |

Fig. 6.1: Storage structure of a one-dimensional array.

However in C++, the subscript of each dimension of an array starts from 0. So in the program, the array is represented as

```cpp
M = {{M[0][0], M[0][1], M[0][2]], [M[1][0], M[1][1], M[1][2]}};
```

| M[0][0] | M[0][1] | M[0][2] |
| :--- | :--- | :--- |
| M[1][0] | M[1][1] | M[1][2] |
| \text{First row} | \text{Second row} | |

Fig. 6.2: Storage structure of two-dimensional array.

Element M[1][0], with 1 as its row subscript and 0 as its column subscript, denotes the first element of the second row of the matrix. A two-dimensional array is stored by rows in memory. That is, the first row is stored first, and then the second, and so on. The elements of each row are stored according to their column subscripts. This storage method is also called row-major storage. For an n-dimensional array, we use a similar method to order the array elements. We view the subscripts of the n dimensions as a counter, where the later subscript is the lower order, and every digit ranges between the lower bound and the upper bound of the corresponding dimension. When the count of digit exceeds the upper bound, a carry is made to the previous digit, and the current and lower digits recount from their respective lower bounds. We can discover that the subscript of the first dimension varies slowest, and the subscript of the last dimension varies quickest. It is noticeable that for each dimension, the lower bound is 0 and the upper bound is the value of the subscript expression in the array declaration minus 1. For example the following array declaration

```cpp
int M[2][3][4];
```

declares a three-dimensional array, and the storage order of elements is indicated in Figure 6.3. In general, arrays with three or more dimensions are rarely used, and the most frequently used is a one-dimensional array.

| M[0][0][0] | M[0][0][1] | M[0][0][2] | M[0][0][3] | M[0][1][0] | M[0][1][1] |
| :--- | :--- | :--- | :--- | :--- | :--- |
| M[0][1][2] | M[0][1][3] | M[0][2][0] | M[0][2][1] | M[0][2][2] | M[0][2][3] |
| M[1][0][0] | M[1][0][1] | M[1][0][2] | M[1][0][3] | M[1][1][0] | M[1][1][1] |
| M[1][1][2] | M[1][1][3] | M[1][2][0] | M[1][2][1] | M[1][2][2] | M[1][2][3] |

**Fig. 6.3:** Storage structure of a three-dimensional array.
