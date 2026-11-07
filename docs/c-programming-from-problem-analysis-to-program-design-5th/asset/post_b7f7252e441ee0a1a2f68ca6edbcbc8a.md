
| Expression | Effect |
| --- | --- |
| `strVar.capacity()` | Returns the size of the storage allocated for strVar. |
| `strVar.erase(pos);` | pos is a parameter of type `string::size_type`.<br><br>Removes all of the characters from strVar starting at index pos. |
| `strVar.resize(n, ch);` | Changes the size of storage allocation for strVar to n. If n is less than the current storage size of strVar, the storage size of the string is truncated to n. If n is greater than the current storage size, the string is expanded to size n and the additional space is filled with copies of the character specified by the char variable ch. |

## Random Number Generator

To generate a random number, you can use the C++ function `rand`. To use the function `rand`, the program must include the header file `cstdlib`. The header file `cstdlib` also contains the constant `RAND_MAX`. Typically, the value of `RAND_MAX` is 32767. To find the exact value of `RAND_MAX`, check your system’s documentation. The function `rand` generates an integer between 0 and `RAND_MAX`. The following program illustrates how to use the function `rand`. It also prints the value of `RAND_MAX`:

```cpp
#include <iostream>
#include <cstdlib>
#include <iomanip>

using namespace std;

int main()
{
    cout << fixed << showpoint << setprecision(5);
    cout << "The value of RAND_MAX: " << RAND_MAX << endl;
    cout << "A random number: " << rand() << endl;
    cout << "A random number between 0 and 9: "
         << rand() % 10 << endl;
    cout << "A random number between 0 and 1: "
         << static_cast<double> (rand())
             / static_cast<double> (RAND_MAX)
         << endl;

    return 0;
}
```

### Sample Run:

```text
The value of RAND_MAX: 32767
A random number: 41
A random number between 0 and 9: 7
A random number between 0 and 1: 0.19330
```

## Container Types

Containers are used to manage objects of a given type. The STL containers are divided into three categories:

- Sequence containers (also called sequential containers)
- Associative containers
- Container adapters

This appendix discusses sequence and container adapters.

### Sequence Containers

Every object in a sequence container has a specific position. The three predefined sequence containers are:

- vectors
- deque
- lists

Before discussing container types in general, let us first briefly describe the sequence container vector. We do so because vector containers are similar to arrays and thus can be processed like arrays. Also, with the help of vector containers, we can describe several properties that are common to all containers. In fact, all containers use the same names for the common operations. Of course, there are operations that are specific to a container, which will be discussed when describing a specific container.

### Sequence Container: Vectors

A vector container stores and manages its objects in a dynamic array. Because an array is a random access data structure, the elements of a vector can be accessed randomly. Item insertion at the beginning or middle of an array is time consuming, especially if the array is large. However, inserting an item at the end is quite fast.

> **NOTE**
>
> Chapter 10 briefly introduced the class `vector` and explained how to declare a vector object and manipulate the data in that object. However, to make this appendix a stand-alone section, we repeat some of the material in Chapter 10. We also provide a detailed discussion of the class `vector`.

The name of the class that implements the vector container is vector. (Recall that containers are class templates.) The name of the header file containing the class vector is vector. Thus, to use a vector container in a program, the program must include the following statement:

```cpp
#include <vector>
```

Furthermore, to define an object of type vector, we must specify the type of the object because the class vector is a class template. For example, the statement:

```cpp
vector<int> intList;
```

declares intList to be a vector and the component type is int. Similarly, the statement:

```cpp
vector<string> stringList;
```

declares stringList to be a vector container and the component type is string.

### DECLARING VECTOR OBJECTS

The class vector contains several constructors, including the default constructor. Therefore, a vector container can be declared and initialized several ways. Table H-1 describes how a vector container of a specific type can be declared and initialized.

**TABLE H-1** Various Ways to Declare and Initialize a Vector Container

| Statement | Effect |
|---|---|
| `vector<elemType> vecList;` | Creates the empty vector container `vecList`. (The default constructor is invoked.) |
| `vector<elemType> vecList (otherVecList);` | Creates the vector container `vecList`, and initializes `vecList` to the elements of the vector `otherVecList`. `vecList` and `otherVecList` are of the same type. |
| `vector<elemType> vecList(size);` | Creates the vector container `vecList` of size `size`. `vecList` is initialized using the default constructor. |
| `vector<elemType> vecList(n, elm);` | Creates the vector container `vecList` of size `n`. `vecList` is initialized using `n` copies of the element `elm`. |
| `vector<elemType> vecList(beg, end);` | Creates the vector container `vecList`. `vecList` is initialized to the elements in the range `[beg, end)`, that is, all the elements in range `beg . . . end-1`. Both `beg` and `end` are pointers, called iterators in STL terminology. (Later in this appendix, we explain how iterators are used.) |

Now that we know how to declare a vector sequence container, let us now discuss how to manipulate the data stored in a vector container. In order to manipulate the data in a vector container, we must know the following basic operations:

- Item insertion
- Item deletion
- Stepping through the elements of a vector container

The elements in a vector container can be accessed directly by using the operations given in Table H-2. The name of the function is shown in bold.

**TABLE H-2** Operations to Access the Elements of a Vector Container

| Expression | Description |
|---|---|
| `vecList.at(index)` | Returns the element at the position specified by *index*. |
| `vecList[index]` | Returns the element at the position specified by *index*. |
| `vecList.front()` | Returns the first element. (Does not check whether the container is empty.) |
| `vecList.back()` | Returns the last element. (Does not check whether the container is empty.) |

From Table H-2, it follows that the elements in a vector can be processed just as they can in an array; see Example H-1. (Recall that in C++, arrays start at location 0. Similarly, the first element in a vector is at location 0.)

### EXAMPLE H-1

Consider the following statement, which declares `intList` to be a vector container of size 5 and the element type is `int`.

```cpp
vector<int> intList(5);
```

You can use a loop, such as the following, to store elements into `intList`:

```cpp
for (int j = 0; j < 5; j++)
    intList[j] = j;
```

Similarly, you can use a `for` loop to output the elements of `intList`.

The class `vector` also contains member functions that can be used to find the number of elements currently in the container, the maximum number of elements that can be inserted into a container, and so on. Table H-3 describes some of these operations. The name of the function is shown in bold. (Suppose that `vecCont` is a vector container.)

**TABLE H-3** Operations to Determine the Size of a Vector Container

| Expression | Description |
|---|---|
| `vecCont.capacity()` | Returns the maximum number of elements that can be inserted into the container `vecCont` without reallocation. |
| `vecCont.empty()` | Returns `true` if the container `vecCont` is empty, `false` otherwise. |
| `vecCont.size()` | Returns the number of elements currently in the container `vecCont`. |
| `vecCont.max_size()` | Returns the maximum number of elements that can be inserted into the container `vecCont`. |

The class `vector` also contains member functions that can be used to manipulate the data, as well as insert and delete items, in a vector container. Suppose that `vecList` is a container of type `vector`. Item insertion and deletion in `vecList` are accomplished using the operations given in Table H-4. These operations are implemented as member functions of the class `vector`, and are shown in bold. Table H-4 also shows how these operations are used.

**TABLE H-4** Various Operations on a Vector Container

| Statement | Effect |
|---|---|
| `vecList.clear()` | Deletes all the elements from the container. |
| `vecList.erase(position)` | Deletes the element at the position specified by `position`. |
| `vecList.erase(beg, end)` | Deletes all the elements starting at `beg` until `end-1`. |
