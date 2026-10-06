
# STL Containers 681

In the private section of our header file, we instantiate our mapper object:

```cpp
std::trl::unordered_map<KeyType, ItemType> mapper;
```

The sole purpose of the dummy mapper object is to give us access to its hash function.
We then call the hash map function and store the reference it returns in the variable hashFunction:

```
typename std::trl::unordered_map<KeyType, ItemType>::hasher hashFunction = mapper.hash_function();
```

The returned reference is to the hash function to use our KeyType. Note that the variable-Function is of type hasher. In the C11 standard, hashing functions are functions of this type. They have a single parameter of type KeyType and return an unsigned integer that represents the hash value of the key. The keyword typename is required so that the compiler understands this statement is based on the template parameters.
Because hasher is defined and initialized in the header file, it is available to any method in the HashedDictionary class. When it is used, we need to use the modulo operator, since hashFunction returns an unsigned integer in the range 0 to UINT_MAX—the maximum unsigned integer. After the modulo operator is applied, we can cast the result to the type of integer we need for our dictionary. Thus, we have the following statement:

```cpp
int hashIndex = static_cast<int>(hashFunction(searchKey) % hashTable);
```

The code in Listing C7-3 gives an example of how to use a hash function when it is not part of an AD. This example creates a hash function for string objects. The key of the type determines our hash function, the type of the mapped value is not important; hence we use int.

LISTING C7-3 Alternative definition of a hash function
```cpp
#include <iostream>
#include <string>
#include <trl/unordered_map> // Note header name since this is in trl
using namespace std;
// Create a type since this is a long name to use (optional)
typedef std::trl::unordered_map<string, int> StringKeyMap;
// Create a dummyMap object so we can get its hash function
StringKeyMap dummyMap;
// Capture the hash function for use in program
StringKeyMap::hasher myFunctionName = dummyMap.hash_function();
int main ()
{
    cout << "Hashing a String: " << myFunctionName("Hashing a String:") << endl;
    cout << "Smashing a String: " << myFunctionName("Smashing a String:") << endl;
    return 0;
} // end main
```
Output
Hashing a String: 2084157801917473989
Smashing a String: 1404877508690358083

## C7.2 STL Algorithms

One of the strengths of the STL container library is the set of functions defined in the header `<algorithm>`. These functions are designed to operate on ranges of iterators. In C++ Interlude 6 you saw a few of these: `for_each`, `find`, `count`, `advance`, and `distance`. In most cases, the type of container is not important, but it supports iterators. This makes possible the comparison of different types of containers. For instance, the entries stored in a vector can be compared to those stored in a `map`.

The first group of algorithms search and compare items in a range. They may change a value, you do not modify the structure of the containers. Several algorithms, such as `for_each`, `find`, and `count_if`, apply helper functions to each entry during the traversal in a similar manner to the tree travers presented in Chapter 15. The table below shows one of each function. Most functions have several forms that allow customization of the range entries to process and the functions to use for comparison. Also, STL map operations, such as `upper_bound` and `lower_bound`, can be used as functions and applied to other container types.

| Operation | Description |
|---|---|
| void for_each(iterator start, iterator end, Function func) | Applies to the range specified by start and end. |
| iterator find(iterator start, iterator end, value_type& val) | Returns an iterator to val in the range specified by start and end. |
| iterator find_if(iterator start, iterator end, PredFunction func) | Returns an iterator to the entry between start and end that makes the predicate function true. |
| uint count(iterator start, iterator end, value_type& val) | Counts the number of occurrences of val between start and end. |
| uint count_if(iterator start, iterator end, PredFunction func) | Counts the number of entries between start and end that make the predicate function true. |
| bool equal(iterator start1, iterator end1, iterator start2) | Compares the entries between start1 and end1 to those beginning at start2. Returns true if all items match. |
| value_type& min(value_type item1, value_type& item2) | Returns the minimum of item1 and item2. |
| value_type& min_element(iterator start, iterator end) | Returns the minimum value in the range from start to end. |
| value_type& max(value_type item1, value_type& item2) | Returns the maximum of item1 and item2. |
| value_type& max_element(iterator start, iterator end) | Returns the maximum value in the range from start to end. |

The sequence-modification algorithms change the entries stored in a container within a range specified by two iterators. The entries can be either

- Replaced by a specific value using fill
- Copied or moved to new locations using copy or move
- Removed based on specified conditions using remove, or
- Have operations applied to them transform and the syntax used to invoke them.

The following table lists a few of the more common operations and

# STL Sequence Modification Algorithms

| Operation | Description |
| --- | --- |
| iterator copy(iterator start1, iterator end1, iterator start2) | Copies the entries within the range start1 to end1 to positions at start2 the same or other container. Returns an iterator to the last entry copied. |
| iterator copy_backward(iterator start1, iterator end1, iterator start2) | Copies the entries within the range start1 to end1 to positions at start2 (if ranges over the same container). Copies entries at end1 - 1. Returns an iterator to the last entry copied. |
| void swap(value_type& item1, value_type& item2) | Swaps the values of two objects, item1 and item2. |
| iterator transform(iterator start1, iterator end1, iterator start2, UnaryOperator op) | Applies the unary operator to entries within the range start1 to end1 and places the result in elements beginning at start2. Returns an iterator to the last entry copied. |
| iterator transform(iterator start1, iterator end1, iterator start2, BinaryOperator op) | Uses items within the range start1 to end1 as the left-hand operand and the entries beginning at start2 as the right-hand operand. |
| void fill(iterator start1, iterator end1, value_type& val) | Sets all entries within the range start1 to end1 the value val. |

The STL algorithm library provides a number of operations that perform sorting or heap operations on a range of elements. It also includes operations, such as partition and nth_element that can be used to implement user-developed sorting algorithms.

# STL Sorting and Heap Algorithms

| Operation | Description |
| --- | --- |
| void sort(iterator start, iterator end) | Sorts entries within the range start to end into ascending order. | (continues)

# C++ INTERLUDE 7 The Standard Template Library

```cpp
void stable_sort(iterator start, iterator end)

iterator partition(iterator start, iterator end, PredFunction func)

iterator partition_stable(iterator start, iterator end, PredFunction func)

void nth_element(iterator start, iterator nth, iterator end)

void make_heap(iterator start, iterator end)

void push_heap(iterator start, iterator end)

void pop_heap(iterator start, iterator end)

void sort_heap(iterator start, iterator end)
```

Sorts entries within the range start to end into ascending order but has stability in ordering—that is, the relative order of equal values is maintained.

Rearranges all entries within the range start to end so that those that make the predicate function true are before those for which the function is false.

Behaves as the same partition, but has stability in ordering—that is, the relative order of equal values is maintained.

Rearranges the entries within the range start to end so that the entry in position nth is in the correct sorted position—that is, it is in the nth position in the sorted sequence.

Rearrange the entries in the range start to end to form a heap.

Assumes that the entries within the range start to end - 1 form a heap and places the entry at position end into the correct location in the heap, extending the heap to position end.

Moves the value at position start to position end - 1 and rebuilds the heap in the range start to end - 2 inclusive.

Assumes that the entries within the range start to end - 1 form a heap and turns the heap back into a sorted container.
