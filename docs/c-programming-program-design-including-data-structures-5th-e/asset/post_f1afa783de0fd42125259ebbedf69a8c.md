
the third element of `intList`. The statement in Line 25 inserts 88 into `intList` at the position specified by the iterator `listIt`. Because `listIt` points to the component at position 2 (the third element of `intList`), 88 is inserted at position 2 in `intList`; that is, 88 becomes the third element of `intList`. The statements in Lines 27 and 28 output the modified `intList`.

## Member Functions Common to All Containers

The previous section discussed vector containers. This section discusses operations that are common to all containers. For example, every container class has the default constructor, several constructors with parameters, the destructor, a function to insert an element into a container, and so on.

Recall that a class encapsulates data and operations on that data into a single unit. Because every container is a class, several operations are directly defined for a container and are provided as part of the definition of the class. Also, recall that the operations to manipulate the data are implemented with the help of functions and are called member functions of the class. Table 22-5 describes the member functions that are common to all containers; that is, these functions are included as members of the class template implementing the container.

Suppose ct, ct1, and ct2 are containers of the same type. In Table 22-5, the name of the function is shown in bold. This table also shows how a function is called.

**TABLE 22-5** Operations Common to All Containers

| Member function | Description |
|---|---|
| Default constructor | Initializes the object to an empty state. |
| Constructor with parameters | In addition to the default constructor, every container has constructors with parameters. We will describe these constructors when we discuss a specific container. |
| Copy constructor | Executes when an object is passed as a parameter by value and when an object is declared and initialized using another object of the same type. |
| Destructor | Executes when the object goes out of scope. |
| `ct.empty()` | Returns `true` if container `ct` is empty, `false` otherwise. |
| `ct.size()` | Returns the number of elements currently in container `ct`. |
| `ct.max_size()` | Returns the maximum number of elements that can be inserted in container ct. |
| `ct1.swap(ct2)` | Swaps the elements of containers ct1 and ct2. |
| `ct.begin()` | Returns an iterator to the first element into container ct. |
| `ct.end()` | Returns an iterator to the position after the last element into container ct. |
| `ct.rbegin()` | Reverse begin. Returns a pointer to the last element into container ct. This function is used to process the elements of ct in reverse. |
| `ct.rend()` | Reverse end. Returns a pointer to the position before the first element into container ct. |
| `ct.insert(position, elem)` | Inserts elem into container ct at the position specified by position. Note that here, position is an iterator. |
| `ct.erase(beg, end)` | Deletes all of the elements between beg...end-1 from container ct. Both beg and end are iterators. |
| `ct.clear()` | Deletes all of the elements from the container. After a call to this function, container ct is empty. |
| **Operator functions** | |
| `ct1 = ct2` | Copies the elements of ct2 into ct1. After this operation, the elements in both containers are the same. |
| `ct1 == ct2` | Returns `true` if containers ct1 and ct2 are equal, `false` otherwise. |
| `ct1 != ct2` | Returns `true` if containers ct1 and ct2 are not equal, `false` otherwise. |

> **NOTE** Because these operations are common to all containers, when discussing a specific container, to save space, these operations will not be listed again.

## Member Functions Common to Sequence Containers

The previous section described the member functions that are common to all containers. In addition to these member functions, Table 22-6 describes the member functions that are common to all sequence containers, that is, containers of type `vector`, `deque`, and `list`. The name of the function is shown in bold. (Suppose that `seqCont` is a sequence container.)

**TABLE 22-6** Member Functions Common to All Sequence Containers

| Expression | Description |
|---|---|
| `seqCont.insert(position, elem)` | A copy of `elem` is inserted at the position specified by the iterator position. The position of the new element is returned. |
| `seqCont.insert(position, n, elem)` | `n` copies of `elem` are inserted at the position specified by the iterator position. |
| `seqCont.insert(position, beg, end)` | A copy of the elements, starting at `beg` until `end−1`, is inserted into `seqCont` at the position specified by the iterator position. Also, `beg` and `end` are iterators. |
| `seqCont.push_back(elem)` | A copy of `elem` is inserted into `seqCont` at the end. |
| `seqCont.pop_back()` | Deletes the last element. |
| `seqCont.erase(position)` | Deletes the element at the position specified by the iterator position. |
| `seqCont.erase(beg, end)` | Deletes all of the elements starting at `beg` until `end−1`. Both `beg` and `end` are iterators. |
| `seqCont.clear()` | Deletes all of the elements from the container. |
| `seqCont.resize(num)` | Changes the number of elements to `num`. If `size()` grows, the new elements are created by the default constructor. |
| `seqCont.resize(num, elem)` | Changes the number of elements to `num`. If `size()` grows, the new elements are copies of `elem`. |

## The copy Algorithm

Example 22-4 used a `for` loop to output the elements of a vector container. The STL provides a convenient way to output the elements of a container with the help of the function copy. The function copy is provided as a part of the generic algorithm and can be used with any container type. Because we frequently need to output the elements of a container, before continuing with our discussion of containers, let us describe this function.

The function copy does more than output the elements of a container. In general, it allows us to copy the elements from one place to another. For example, to output the elements of a vector or to copy the elements of a vector into another vector, we can use the function copy. The prototype of the function template copy is:

```
template <class inputIterator, class outputIterator>
outputIterator copy(inputIterator first1, inputIterator last,
                     outputIterator first2);
```

The parameter `first1` specifies the position from which to begin copying the elements; the parameter `last` specifies the end position. The parameter `first2` specifies where to copy the elements. Therefore, the parameters `first1` and `last` specify the source; parameter `first2` specifies the destination.

Note that the elements within the range `first1...last-1` are copied.

The definition of the function template copy is contained in the header file algorithm. Thus, to use the function copy, the program must include the statement:

```
#include <algorithm>
```

The function copy works as follows. Consider the following statement:

```
int intArray[] = {5, 6, 8, 3, 40, 36, 98, 29, 75};
```

This statement creates an array `intArray` of nine components. Here `intArray[0] = 5`, `intArray[1] = 6`, and so on.

The statement:

```
vector<int> vecList(9);
```

creates an empty container of nine components of type vector and the element type `int`.

Recall that the array name, `intArray`, is actually a pointer and contains the base address of the array. Therefore, `intArray` points to the first component of the array, `intArray + 1` points to the second component of the array, and so on.

Now consider the statement:

```
copy(intArray, intArray + 9, vecList.begin());
```

This statement copies the elements starting at the location `intArray`, which is the first component of the array `intArray`, until `intArray + 9 - 1` (that is, `intArray + 8`).
