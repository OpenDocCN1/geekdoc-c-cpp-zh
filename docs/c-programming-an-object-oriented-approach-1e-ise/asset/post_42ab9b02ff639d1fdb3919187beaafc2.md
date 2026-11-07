
### Program 19.27 Using sorting algorithms (Continued)

```
Vector after sorting in ascending order
10  11  13  15  17  18

Vector after sorting in descending order
18  17  15  13  11  10
```

We now test the `binary_search()` algorithm. The sequence must be sorted for this algorithm to work correctly. Program 19.28 shows a simple example in which we create a vector of integer values, we sort it, and then we search the vector for two values: one in the vector and the other not in the vector.

### Program 19.28 Using a binary search algorithm

```cpp
/**************************************************************
 * A program that uses binary search on a vector                *
 **************************************************************/
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

int main()
{
    // Instantiation of a vector object
    vector<int> vec;
    // Adding six elements to the vector
    vec.push_back(17);
    vec.push_back(10);
    vec.push_back(13);
    vec.push_back(18);
    vec.push_back(15);
    vec.push_back(11);
    // Sorting the vector
    sort(vec.begin(), vec.end());
    // Searching vector for two values
    cout << "Found 10 in vector? " << boolalpha;
    cout << binary_search(vec.begin(), vec.end(), 10) << endl;
    cout << "Found 19 in vector? " << boolalpha;
    cout << binary_search(vec.begin(), vec.end(), 19) << endl;
    return 0;
}

Run:
Found 10 in vector? true
Found 19 in vector? false
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_925_0.png)

### Figure 19.16 Graphical representation of set union

Figure 19.16 shows union operations applied to *first* and *second* sets. The result is the shaded area. The union is a set that includes all elements in *first* and *second*.

Program 19.29 shows how we can apply the union operation on the two sets (*first* and *second*).

### Program 19.29 Finding the union of two sets

```cpp
/***************************************************************
 * A program that finds the union of two sets                    *
 ***************************************************************/
#include <set>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

// Print function
void print(int value)
{
    cout << value << " ";
}

int main()
{
    // Creation of the first set
    set<int> first;
    first.insert(10);
    first.insert(19);
    first.insert(14);
    first.insert(17);
    first.insert(13);
    cout << "Elements of first set" << endl;
    for_each(first.begin(), first.end(), print);
    cout << endl << endl;
    // Creation of the second set
    set<int> second;
    second.insert(16);
    second.insert(14);
    second.insert(13);
    second.insert(11);
    second.insert(20);
    cout << "Elements of second set" << endl;
    for_each(second.begin(), second.end(), print);
    cout << endl << endl;
    // Finding the union of two sets and storing in a vector
    vector<int> temp(10);
    vector<int>::iterator iter;
    vector<int>::iterator endIter;
    endIter = set_union(first.begin(), first.end(), second.begin(),
                        second.end(), temp.begin());
    // Copying elements from the vector to the result set
    set<int> result;
    for (iter = temp.begin(); iter != endIter; iter++)
    {
        result.insert(*iter);
    }
    cout << "Elements of result set" << endl;
    for_each(result.begin(), result.end(), print);
    cout << endl << endl;
    return 0;
}

Run:
Elements of first set
10  13  14  17  19

Elements of second set
11  13  14  16  20

Elements of result set
10  11  13  14  16  17  19  20
```

In Program 19.29 the size of the target sequence must be large enough to accommodate the result. This is not possible with a set because any set which is created is empty. To solve the problem, we have created a vector to temporarily hold the result of an operation and then copied the part of the vector that holds the result to the resulting set. Figure 19.17 shows the process we have used.

## 19.7.4 Numeric Algorithms

There are a few **numeric algorithm**, defined in the `<numeric>` header file, that perform simple arithmetic operations on the elements of a container or containers. Note that these algorithms do not have to be applied on arithmetic types (such as *int* or *double*); as long as the corresponding operation is defined for a type, these algorithms can be applied to them. Table 19.9 shows one commonly used numeric algorithm.

### Program 19.30 Testing the accumulate algorithm (Continued)

```cpp
24  vec.push_back(15);
25  vec.push_back(17);
26  for_each(vec.begin(), vec.end(), print);
27  cout << endl;
28  // Calculate the sum and print it
29  int sum = accumulate(vec.begin(), vec.end(), 0);
30  cout << "Sum of elements: " << sum;
31  return 0;
32  }

Run:
17 10 13 13 18 15 17
Sum of elements: 103
```

## Key Terms

- algorithm
- associative container
- bidirectional iterator
- container
- container adapter
- deque class
- forward iterator
- input iterator
- iterator
- list class
- map
- mutating algorithm
- non-mutating algorithm
- numeric algorithm
- output iterator
- priority_queue class
- queue class
- random-access iterator
- sequence container
- set
- sorting algorithm
- stack class
- vector class

## Summary

The Standard Template Library (STL) is the result of years of research to solve two important issues: reusability of software and creation of components each with a distinct functionality. STL is made of four components: iterators, containers, functions, and algorithms.

Iterators are tools that allow us to access objects in a container. They are based on the pointer concept that allows us to reference objects using their addresses.

A sequence container preserves the original order of items added to the container. It consists of three classes: *vector*, *deque*, and *list*. Container adapters include *stack*, *queue*, and *priority_queue* classes. Associative containers hold elements stored and retrieved by a key. We discussed two classes of associative containers: *set* and *map*.

STL uses either a pointer to function or a function object in algorithms. If an algorithm uses a pointer to function, the user needs to provide the function definition. If an algorithm uses a function object, it is normally defined in the collection.

Algorithms consist of template global functions that can be applied to any container type that supports the iterators required by the algorithm. We have divided algorithms into four groups: non-mutating, mutating, sorting, and numeric.

## Problems

- **PR-1.** Write the definition of a generic function that prints the value of all elements in a `vector` of any type.
- **PR-2.** Write the definition of a generic function that prints the value of all elements in a `list` of any type.
- **PR-3.** Write the code to create a vector of 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 values using the `at()` member function.
- **PR-4.** Write the code to create a list of 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 values.
- **PR-5.** Write the statements to swap the values at index 2 and index 3 in a vector of type integer named `vec`.
- **PR-6.** Write the statements to swap the values of second and third elements in a list of type integer named `lst`.
- **PR-7.** The `push_front` operation is not defined for a vector. Write code to insert a value at the front of a vector of type integer.
- **PR-8.** The `pop_front` operation is not defined for a vector. Write code to remove the first element from a vector of type integer.
- **PR-9.** The `remove` function is not defined for a vector. Write code to simulate the remove function for a vector.
- **PR-10.** Assume we insert the following integer values into an empty priority queue: 14, 24, 76, 18, 20, and 54. We then pop two integers. What is the next integer to be popped?
- **PR-11.** Assume we insert the following values into a set: 20, 17, 20, 14, 15, 19, 17, and 10. What would be printed from the `size()` member function after all insertions?
- **PR-12.** Assume we insert the following pairs into a `map`: (20, 10), (14, 40), and (17, 3). What is the order of these items in the map?
- **PR-13.** Assume we have the following items in a set named `st`: 20, 14, 18, 22, 76. Write the code to print 18 and 22.
- **PR-14.** Assume we have inserted the pairs (15, 10), (16, 10), (6, 16), and (12, 8) into a `map` named `mp`. What would be printed from the following code?

```cpp
cout << mp[6] << endl;
cout << mp[16] << endl;
cout << mp[10] << endl;
```

- **PR-15.** Write the code to create a map and use the `insert` member function to insert the following pairs in it: (3, 10), (5, 12), and (7, 8).

## Programs

- **PRG-1.** Since the pointers in an array are compatible with random-access iterators, we can use some algorithms defined in the STL with arrays. Write a program that initializes an array of five elements, defines a print function, and uses the `for_each` algorithm to print the values in the array.
- **PRG-2.** The `max` and `min` functions defined in `<algorithm>` can be used to compare any two objects for which the less-than (`<`) and greater-than (`>`) operators are defined. Use these functions in a small program to compare two integers, two doubles, and two strings. These two templated functions are defined as shown below:
