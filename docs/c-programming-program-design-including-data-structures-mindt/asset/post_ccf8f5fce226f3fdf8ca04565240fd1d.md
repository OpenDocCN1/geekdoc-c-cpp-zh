
Now that we know how to declare a vector sequence container, let us discuss how to manipulate the data stored in a vector container. In order to manipulate the data in a vector container, we must know the following basic operations:

- Item insertion
- Item deletion
- Stepping through the elements of a vector container

The elements in a vector container can be accessed directly by using the operations given in Table 21-2.

## TABLE 21-2 Operations to Access the Elements of a Vector Container

| Expression | Description |
|---|---|
| `vecList.at(index)` | Returns the element at the position specified by `index`. |
| `vecList[index]` | Returns the element at the position specified by `index`. |
| `vecList.front()` | Returns the first element. (Does not check whether the container is empty.) |
| `vecList.back()` | Returns the last element. (Does not check whether the container is empty.) |

From Table 21-2, it follows that the elements in a vector can be processed just as they can in an array. See Example 21-1. (Recall that in C++, arrays start at location 0. Similarly, the first element in a vector container is at location 0.)

## EXAMPLE 21-1

Consider the following statement, which declares `intList` to be a vector container of size 5 with an element type of `int`:

```cpp
vector<int> intList(5);
```

You can use a loop, such as the following, to store elements into `intList`:

```cpp
for (int j = 0; j < 5; j++)
    intList[j] = j;
```

Similarly, you can use a `for` loop to output the elements of `intList`.

The `class vector` also contains member functions that can be used to find the number of elements currently in the container, the maximum number of elements that can be inserted into a container, and so on. Table 21-3 describes some of these operations. In this table, `vecCont` is a vector container.

## TABLE 21-3 Operations to Determine the Size of a Vector Container

| Expression | Description |
|---|---|
| `vecCont.capacity()` | Returns the maximum number of elements that can be inserted into the container `vecCont` without reallocation. |
| `vecCont.empty()` | Returns `true` if the container `vecCont` is empty, `false` otherwise. |
| `vecCont.size()` | Returns the number of elements currently in the container `vecCont`. |
| `vecCont.max_size()` | Returns the maximum number of elements that can be inserted into the container `vecCont`. |

The `class vector` also contains member functions that can be used to manipulate the data, as well as insert and delete items, in a vector container. Suppose that `vecList` is a container of type `vector`. Item insertion and deletion in `vecList` are accomplished using the operations given in Table 21-4. These operations are implemented as member functions of the `class vector`. Table 21-4 also shows how these operations are used.

## TABLE 21-4 Various Operations on a Vector Container

| Statement | Effect |
|---|---|
| `vecList.clear();` | Deletes all of the elements from the container. |
| `vecList.erase(position);` | Deletes the element at the position specified by `position`. |
| `vecList.erase(beg, end);` | Deletes all of the elements starting at `beg` until `end - 1`. |
| `vecList.insert(position, elem);` | A copy of `elem` is inserted at the position specified by `position`. The position of the new element is returned. |
| `vecList.insert(position, n, elem);` | `n` copies of `elem` are inserted at the position specified by `position`. |
| `vecList.insert(position, beg, end);` | A copy of the elements, starting at `beg` until `end - 1`, is inserted into `vecList` at the position specified by `position`. |
| `vecList.push_back(elem);` | A copy of `elem` is inserted into `vecList` at the end. |
| `vecList.pop_back();` | Deletes the last element. |
| `vecList.resize(num);` | Changes the number of elements to `num`. If the size increases, the default constructor creates the new elements. |
| `vecList.resize(num, elem);` | Changes the number of elements to `num`. If the size increases, the new elements are copies of `elem`. |

> In Table 21-4, the identifiers `position`, `beg`, and `end` in STL terminology are called iterators. An iterator is just like a pointer. In general, iterators are used to step through the elements of a container. In other words, with the help of an iterator, we can walk through the elements of a container and process them one at a time. Because iterators are an integral part of the STL, they are discussed in the section “Iterators” located later in this chapter.

Example 21-1 used a `for` loop and the array subscripting operator, `[]`, to access the elements of `intList`. We declare `intList` to be a vector object of size 5. Does this mean that we can store only five elements in `intList`? The answer is no. We can, in fact, add more elements to `intList`. However, because when we declared `intList` we specified the size to be 5, in order to add elements past position 4, we use the function `push_back`. Furthermore, if we initially declare a vector object and do not specify its size, then to add elements to the vector object, we use the function `push_back`. Example 21-2 explains how to use the function `push_back`.

## EXAMPLE 21-2

The following statement declares `intList` to be a vector object of size 0:

```cpp
vector<int> intList;
```

To add elements to `intList`, we can use the function `push_back` as follows:

```cpp
intList.push_back(34);
intList.push_back(55);
```

After these statements execute, the size of `intList` is 2 and

```cpp
intList = {34, 55}
```

In Example 21-2, because `intList` is declared to be of size 0, we use the function `push_back` to add elements to `intList`. However, we can also use the `resize` function to increase the size of `intList` and then use the array subscripting operator. For example, suppose that `intList` is declared as in Example 21-2. Then, the following statement sets the size of `intList` to 10:

```cpp
intList.resize(10);
```

Similarly, the following statement increases the size of `intList` by 10:

```cpp
intList.resize(intList.size() + 10);
```

However, at times, the `push_back` function is more convenient because it does not need to know the size of the vector; it simply adds the elements at the end.

Next, we describe how to declare an iterator in a vector container.

## DECLARING AN ITERATOR TO A VECTOR CONTAINER

The class `vector` contains a `typedef` `iterator`, which is declared as a `public` member. An iterator to a vector container is declared using the `typedef` `iterator`. For example, the statement

```cpp
vector<int>::iterator intVecIter;
```

declares `intVecIter` to be an iterator in a vector container of type `int`.

Because **iterator** is a typedef defined inside the **class vector**, we must use the container name (which is **vector**), the container element type, and the scope resolution operator to use the typedef **iterator**.

The expression

```cpp
++intVecIter
```

advances the iterator **intVecIter** to the next element in the container, and the expression

```cpp
*intVecIter
```

returns the element at the current iterator position.

Note that these operations are the same as the operations on pointers, discussed in Chapter 12. Recall that when used as a unary operator, `*` is called the dereferencing operator.

We now discuss how to use an iterator in a vector container to manipulate the data stored in the vector container.

Suppose that we have the following statements:

```cpp
vector<int> intList;                          // Line 1
vector<int>::iterator intVecIter;             // Line 2
```

The statement in Line 1 declares `intList` to be a vector container, and the element type is `int`. The statement in Line 2 declares `intVecIter` to be an iterator in a vector container whose element type is `int`.

## CONTAINERS AND THE FUNCTIONS begin AND end

Every vector has the member functions `begin` and `end`. The function `begin` returns the position of the first element in the container; the function `end` returns the position of one past the last element in the container. Also, these functions have no parameters.

After the following statement executes

```cpp
intVecIter = intList.begin();
```

the iterator `intVecIter` points to the first element in the container `intList`.

The following `for` loop outputs the elements of `intList` to the standard output device.

```cpp
for (intVecIter = intList.begin(); intVecIter != intList.end();
                             ++intVecIter)
    cout << *intVecIter << " ";
```

Example 21-3 shows how the function `insert` works with vector objects.
