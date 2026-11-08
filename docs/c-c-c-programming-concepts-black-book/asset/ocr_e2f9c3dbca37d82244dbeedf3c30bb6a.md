say 100 of them exist. Typical example is sorting numbers in a file. In this case, if a programmer wishes to sort 100 values at the same time, then imagine how difficult it would be if there were no concepts of arrays, as the programmer need to keep the values in 100 different variables. Now, the programmer can group the variables into an array and access them with array indices.

However, one disadvantage of arrays is that they are pre-allocated, that is, they allocate memory as soon as they are declared, which is good if the data size is known in advance; else, a lot of memory space is wasted at runtime. The space wastage in case of arrays is due to the programmer's overcommitting the size of array while writing the program. In spite of the fact that the entire size of an array will hardly be used at runtime, some amateur programmers define the size of an array by taking a bigger value. This is primarily done due to the fear that the array might run out of space, but this mostly results in the space wastage during runtime.

> **NOTE**
> 
> In Standard C++, an array is not the only means of grouping similar types of elements or values. We can also use vectors, which are part of Standard Template Library (STL). We learn more about vectors in chapter 18.

We can define arrays of any C++ data type, starting from the basic data types to user-defined data types. Following is a declaration of an array:

```
```cpp
data_type array[size];
```
```

Now, let's define an array of size 10. As soon as the processing begins, 10 memory locations each of size equal to that of data type are contiguously allocated in the memory. The base address of the array can be obtained by the array name or the address of its first member. Note that array indexing starts from 0 and ends at size-1 position. Let's take a real array declaration and see what these values are:

| Array declaration: | int array[10]; |
| :--- | :--- |
| How many elements: | 10 |
| First Element in: | array[0] |
| Last Element in: | array[9] |
| Address of the array: | array or &array[0] |

In the preceding array, each cell corresponds to an integer variable, as if they are grouped together.

Now, consider the following program:

```
```cpp
1:// Demonstrating arrays in C++
2:#include <iostream>
3:using namespace std;
4:#define MAX 10
5:
6:int main ()
7:{
8: int num[MAX];
9: float average = 0.0;
10:
11:     for (int i=0; i < MAX; i++) {
12:         cout<<"\nEnter a number: ";
13:         cin >> num[i];
14:         average += num[i];
15:     }
16:     average = average / MAX;
17:     cout<<"\nThe average of the array elements are "<<average<<endl;
18:     return 0;
19:}
```
```

The preceding program declares an integer array at line number 8 and the size of the array is specified by a macro MAX with value 10. On execution, this program prompts a user to input 10 integers one by one. Then it calculates and displays the average of the input set as entered by the user. Following is the output of the preceding program: