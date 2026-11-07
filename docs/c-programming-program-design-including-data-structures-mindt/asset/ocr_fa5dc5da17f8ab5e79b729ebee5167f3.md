Because **first** and **second** point to the same array, after the statement

```
```cpp
delete [] second;
```
```

executes, **first** becomes invalid; that is, **first** (as well as **second**) are now dangling pointers. Therefore, if the program later tries to access the memory pointed to by **first**, either the program will access the wrong memory or it will terminate in an error. This case is an example of a shallow copy. More formally, in a **shallow copy**, two or more pointers of the same type point to the same memory; that is, they point to the same data.

On the other hand, suppose that instead of the earlier statement, **second = first;** (in Line A), we have the following statements:

```
```cpp
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```
```

The first statement creates an array of 10 components of type **int**, and the base address of the array is stored in **second**. The second statement copies the array pointed to by **first** into the array pointed to by **second** (see Figure 12-12).

![](bbox=[0.183, 0.46, 0.909, 0.563])

**FIGURE 12-12**  *first* and *second* both pointing to their own data

Both **first** and **second** now point to their own data. If **second** deletes its memory, there is no effect on **first**. This case is an example of a deep copy. More formally, in a **deep copy**, two or more pointers of the same type each point to their own copy of the data.

From the preceding discussion, it follows that you must know when to use a shallow copy and when to use a deep copy.

# Classes and Pointers: Some Peculiarities

In a previous section, we discussed how to use the arrow notation to access class members via the pointer if a pointer variable is of a class type. Because a class can have pointer member variables, this section discusses some peculiarities of such classes. To facilitate the discussion, we will use the following class:

```
```cpp
class ptrMemberVarType
{
```
```