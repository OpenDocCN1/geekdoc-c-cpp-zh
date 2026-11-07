declares list to be an array of 10 components and initializes all of the components to 0.
The statement:

```
```cpp
int list[10] = {8, 5, 12};
```
```

declares list to be an array of 10 components and initializes list[0] to 8, list[1] to 5, list[2] to 12, and all other components to 0. Thus, if all of the values are not specified in the initialization statement, the array components for which the values are not specified are initialized to 0. Note that, here, the size of the array in the declaration statement does matter. For example, the statement:

```
```cpp
int list[] = {5, 6, 3};
```
```

declares list to be an array of three components and initializes list[0] to 5, list[1] to 6, and list[2] to 3. In contrast, the statement:

```
```cpp
int list[25] = {4, 7};
```
```

declares list to be an array of 25 components. The first two components are initialized to 4 and 7, respectively, and all other components are initialized to 0.

Suppose that you have the following statement: int x[5] = {};. Then some compilers may initialize each element of the array x to 0.

When you partially initialize an array, then all of the elements that follow the last uninitialized element must be uninitialized. Therefore, the following statement will result in a syntax error:

```
```cpp
int list[10] = {2, 5, 6, , 8}; //illegal
```
```

In this initialization, because the fourth element is uninitialized, all elements that follow the fourth element must be left uninitialized.

# ## Some Restrictions on Array Processing

Consider the following statements:

```
```cpp
int myList[5] = {0, 4, 8, 12, 16};    //Line 1
int yourList[5];                        //Line 2
```
```

The statement in Line 1 declares and initializes the array myList, and the statement in Line 2 declares the array yourList. Note that these arrays are of the same type and have the same number of components. Suppose that you want to copy the elements of myList into the corresponding elements of yourList. The following statement is illegal:

```
```cpp
yourList = myList;    //illegal
```
```

In fact, this statement will generate a syntax error. C++ does not allow aggregate operations on an array. An aggregate operation on an array is any operation that manipulates the entire array as a single unit.