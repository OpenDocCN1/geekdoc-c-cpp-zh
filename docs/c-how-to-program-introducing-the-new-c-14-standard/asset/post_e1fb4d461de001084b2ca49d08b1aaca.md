
## Answers to Self-Review Exercises

- 1. **19.1**
  - A. referential.
  - B. `new`.
  - C. stack.
  - D. predicate.
  - E. first-in, first-out (FIFO).
  - F. link.
  - G. `delete`.
  - H. queue.
  - I. tree.
  - J. last-in, first-out (LIFO).
  - K. binary.
  - L. root.
  - M. child or subtree.
  - N. leaf.
  - O. inorder, preorder, postorder and level order.

- 2. **19.2** It’s possible to insert a node anywhere in a linked list and remove a node from anywhere in a linked list. Nodes in a stack may only be inserted at the top of the stack and removed from the top of a stack.

- 3. **19.3** A queue data structure allows nodes to be removed only from the head of the queue and inserted only at the tail of the queue. A queue is referred to as a first-in, first-out (FIFO) data structure. A stack data structure allows nodes to be added to the stack and removed from the stack only at the top. A stack is referred to as a last-in, first-out (LIFO) data structure.

- 4. **19.4**
  - A. Classes allow us to instantiate as many data structure objects of a certain type (i.e., class) as we wish.
  - B. Class templates enable us to instantiate related classes, each based on different type parameters—we can then generate as many objects of each template class as we like.
  - C. Inheritance enables us to reuse code from a base class in a derived class, so that the derived-class data structure is also a base-class data structure (with `public` inheritance, that is).
  - D. Private inheritance enables us to reuse portions of the code from a base class to form a derived-class data structure; because the inheritance is `private`, all `public` base-class member functions become `private` in the derived class. This enables us to prevent clients of the derived-class data structure from accessing base-class member functions that do not apply to the derived class.
  - E. Composition enables us to reuse code by making a class object data structure a member of a composed class; if we make the class object a `private` member of the composed class, then the class object’s `public` member functions are not available through the composed object’s interface.

- 5. **19.5** The inorder traversal is

```text
11 18 19 28 32 40 44 49 69 71 72 83 92 97 99
```

The preorder traversal is

```text
49 28 18 11 19 40 32 44 83 71 69 72 97 92 99
```

The postorder traversal is

```text
11 19 18 32 44 40 28 69 72 71 92 99 97 83 49
```

## 20 Searching and Sorting

### Objectives

In this chapter you’ll:

- Search for a given value in an `array` using linear search and binary search.
- Sort an `array` using insertion sort, selection sort and the recursive merge sort algorithms.
- Use Big O notation to express the efficiency of searching and sorting algorithms and to compare their performance.
- Understand the nature of algorithms of constant, linear and quadratic runtime.

### Outline

- 1. **20.1 Introduction**
- 2. **20.2 Searching Algorithms**
  - A. **20.2.1 Linear Search**
  - B. **20.2.2 Binary Search**
- 3. **20.3 Sorting Algorithms**
  - A. **20.3.1 Insertion Sort**
  - B. **20.3.2 Selection Sort**
  - C. **20.3.3 Merge Sort (A Recursive Implementation)**
- 4. **20.4 Wrap-Up**
- 1. **Summary**
- 2. **Self-Review Exercises**
- 3. **Answers to Self-Review Exercises**
- 4. **Exercises**

### 20.1 Introduction

**Searching** data involves determining whether a value (referred to as the **search key**) is present in the data and, if so, finding the value’s location. Two popular search algorithms are the simple *linear search* ([Section 20.2.1](#)) and the faster but more complex *binary search* ([Section 20.2.2](#)).

**Sorting** places data in ascending or descending order, based on one or more **sort keys**. A list of names could be sorted alphabetically, bank accounts could be sorted by account number, employee payroll records could be sorted by social security number, and so on. You’ll learn about *insertion sort* ([Section 20.3.1](#)), *selection sort* ([Section 20.3.2](#)) and the more efficient, but more complex *merge sort* ([Section 20.3.3](#)). **Figure 20.1** summarizes the searching and sorting algorithms discussed in the book’s examples and exercises. This chapter also introduces **Big O notation**, which is used to characterize an algorithm’s worst-case runtime—that is, how hard an algorithm may have to work to solve a problem.

**Fig. 20.1 Searching and sorting algorithms in this text.**

| Algorithm | Location | Algorithm | Location |
|---|---|---|---|
| **Searching Algorithms** |  | **Sorting Algorithms** |  |
| Linear search | [Section 20.2.1](#) | Insertion sort | [Section 20.3.1](#) |
| Binary search | **Section 20.2.2** | Selection sort | **Section 20.3.2** |
| Recursive linear search | **Exercise 20.8** | Recursive merge sort | **Section 20.3.3** |
| Recursive binary search | **Exercise 20.9** | Bubble sort | **Exercises 20.5–20.6** |
| Binary tree search | **Section 19.6** | Bucket sort | **Exercise 20.7** |
| Linear search (linked list) | **Exercise 19.21** | Recursive quicksort | **Exercise 20.10** |
| `binary_search` standard library function | **Section 16.4.6** | Binary tree sort | **Section 19.6** |
|  |  | `sort` standard library function | **Section 16.4.6** |

### *A Note About This Chapter’s Examples*

The searching and sorting algorithms in this chapter are implemented as function templates that manipulate objects of the `array` class template. To help you visualize how certain algorithms work, some of the examples display `array`-element values throughout the searching or sorting process. These output statements slow an algorithm’s performance and would *not* be included in industrial-strength code.

### 20.2 Searching Algorithms

Looking up a phone number, accessing a website and checking a word’s definition in a dictionary all involve searching through large amounts of data. A searching algorithm finds an element that matches a given search key, if such an element does, in fact, exist. There are, however, a number of things that differentiate search algorithms from one another. The major difference is the amount of *effort* they require to complete the search. One way to describe this *effort* is with Big O notation. For searching and sorting algorithms, this is particularly dependent on the number of data elements.

In **Section 20.2.1**, we present the linear search algorithm then discuss the algorithm’s *efficiency* as measured by Big O notation. In **Section 20.2.2**, we introduce the binary search algorithm, which is much more efficient but more complex to implement.

#### 20.2.1 Linear Search

In this section, we discuss the simple **linear search** for determining whether an *unsorted* `array` (i.e., an `array` with element values that are in no particular order) contains a specified search key. [Exercise 20.8](#) at the end of this chapter asks you to implement a recursive version of the linear search.

#### Function Template `linearSearch`

Function template `linearSearch` (**Fig. 20.2**, lines 10–19) compares each element of an `array` with a *search key* (line 13). Because the array is not in any particular order, it’s just as likely that the search key will be found in the first element as the last. On average, therefore, the program must compare the search key with *half* of the `array`’s elements. To determine that a value is *not* in the `array`, the program must compare the search key to *every* `array` element. Linear search works well for *small* or *unsorted* arrays. However, for large arrays, linear searching is inefficient. If the array is *sorted* (e.g., its elements are in ascending order), you can use the high-speed binary search technique (**Section 20.2.2**).

```cpp
// Fig. 20.2: LinearSearch.cpp
// Linear search of an array.
#include <iostream>
#include <array>
using namespace std;

// compare key to every element of array until location is
// found or until end of array is reached; return location of
// element if key is found or -1 if key is not found
template <typename T, size_t size>
int linearSearch(const array<T, size>& items, const T& key) {
    for (size_t i{0}; i < items.size(); ++i) {
        if (key == items[i]) { // if found
            return i; // return location of key
        }
    }

    return -1; // key not found
}

int main() {
    const size_t arraySize{100}; // size of array
    array<int, arraySize> arrayToSearch; // create array

    for (size_t i{0}; i < arrayToSearch.size(); ++i) {
        arrayToSearch[i] = 2 * i; // create some data
    }

    cout << "Enter integer search key: ";
    int searchKey; // value to locate
    cin >> searchKey;

    // attempt to locate searchKey in arrayToSearch
    int element{linearSearch(arrayToSearch, searchKey)};

    // display results
    if (element != -1) {
        cout << "Found value in element " << element << endl;
    }
    else {
        cout << "Value not found" << endl;
    }
}
```

```text
Enter integer search key: 36
Found value in element 18
```

```text
Enter integer search key: 37
Value not found
```
