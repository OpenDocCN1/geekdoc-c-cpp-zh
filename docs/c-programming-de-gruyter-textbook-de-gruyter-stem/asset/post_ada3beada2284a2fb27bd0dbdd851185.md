
## 10.2 Containers in STL

There are two access patterns in sequential containers: sequential access and random access. You have to access the element sequentially in a container that only supports sequential access, i.e., have to access the first and the second element before accessing the third. However, you can access the elements directly if the container supports random access. Vectors and double queues are random-access containers while lists are sequential-access containers.

There are four associative containers: set, multiset, map, and multimap. An element can be accessed based on its key. Interested readers can refer to books about data structure and STL for more details.

There are seven containers in STL, and they provide the functions of storing, searching, and accessing elements. Besides, stacks, queues, and priority queues are standard data structures, and are necessary in many applications. STL provides three kinds of module called adaptors. Combining adaptors and sequential containers provide the functions of stacks, queues, and priority queues.

### 10.2.1 Sequential Containers

The most widely used sequential container in C++ is the array. However, sometimes more powerful tools are needed. To meet this need, STL implements three sequential containers: vectors, lists, and double queues.

The vector is a powerful extension of the static array. It is very similar to the static array, but it can allocate its storage on demand at runtime.

The list is an implementation of the double-linked list. It is quick to add or remove an element from a list.

The double queue is an extension of the data structure queue. Compared to a standard queue, it can add or remove elements from both ends of the queue.

### 1. Common Interfaces of Sequential Containers

#### a) Adding Elements

There are a number of ways to insert elements into a container. The first one is to use the push() or push_back() methods, which add an element at the front or the end of the container respectively.

The second way is to use the insert() method. It has some variants in different containers. Insert (L, O) adds element O before location L. Insert (L, N, O) inserts element O before location N. Insert (L, i, j) adds all element between location i and j before location L. It is worth mentioning that the insert() method will possibly invalidate all iterators in vectors and double queues, and insert() methods should be used with care.

The third way is to use the assignment operator to add all elements in a container into an empty container.

These three ways are standard ways to add elements into a sequential container. Calling push_front() or push_back(), using insert(), and using the assignment operator are the three standard ways to add elements to a sequential container.

#### b) Removing Elements

There are also a number of ways to remove elements in a container. We should notice to remove elements rather than the container's destructor. The first method is to call pop_front() or pop_back(). They remove the element at the head and the element at the tail of the container, respectively.

The second way is to call the erase() method. erase(L1, L2) removes all elements at location L between locations L1 and L2.

The third way is to call the clear() method, which removes all elements in the container.

Removing elements will also invalidate iterators. erase() and clear() will invalidate the iterators to the deleted elements in list container. The effect of removing elements from the head or the tail of the double queue is the same as the one in list, but removing an element from the middle of a double queue will invalidate all iterators. Removing elements in vectors also invalidate all iterators.

#### c) Traversing the Sequential Container

The iterator is the object-oriented approach to traverse a container. It overloads the dereference operator "*" to return the reference of the element it points to, just as a normal pointer.

#### d) Other Ways to Access Elements in a Sequential Container

Programmer can use methods front() and back() to access the element at the head or the tail of the container respectively. subscript operator "[]" can also be used to directly access elements in the container, which is only available in vectors and double queues. For example, in a double queue A that holds 15 elements, A[7] points to the seventh element in the queue, and A[N] points to the N-th element in A. Table 10.3 demonstrates these methods.

### 2. Vectors

The vector is a variable length linear collection designed to provide rapid access for objects. It is very similar to the static array, but vectors can change their storage size on demand at runtime.

Vectors are powerful containers. They can be used to implement queues, stacks, lists, or other complicated data structures.

#### a) Constructors and Destructors

There are four default constructors in a vector:

```
vector(); //default constructor
vector(size_type n,const T&value=T()); /*initialize a vector of
size n, the second parameter is the initial value of any object,
which is by default an object constructed by T()*/
vector(const vector& x);//copy constructor, initialized with vector x
vector(const_iterator first, const_iterator last); /*create a new
vector from part of a container that supports const_iterator*/
```

As all containers in STL, vectors accommodate the object-oriented mechanism for memory management. All memory used by the vector itself, and the memory used by elements in the vector, are reclaimed by calling their destructors appropriately when the instance is out of scope.

One thing to notice is that removing an element from a vector just removes the element from the vector. It only calls its destructor but does not reclaim the memory.

#### b) Using Vector

##### 1. Querying Status of Vector

There are four methods for querying the status of a vector: size(), max_size(), capacity(), and empty(). Here are their prototypes:

```
size_type size() const; //Returns the size of the vector
size_type max_size() const; //Returns the largest possible size of the vector
size_type capacity() const; //Number of elements for which memory is allocated
bool empty() const; //returns true if the vector's size is 0
```

```
void push_back(const T& x); /* Inserts a new element at the end,
memory would be requested if size is current capacity */
iterator insert(iterator it, const T& x = T()); //Inserts before it
void insert(iterator it,size_type n,const T& x); //Inserts n copies of x before it
void insert(iterator first, const_iterator last); //Inserts the range [first, last) before it
void swap(vector x); //Swaps the contents of two vectors
```

##### 3. Deleting Elements from Vector

Programmers can use pop_back(), erase(), or clear() methods to remove an element from a vector. Here are the prototypes:

```
void pop_back(); //Removes the last element
iterator erase(iterator it); //Erases the element at position it
iterator erase(iterator first, iterator last) //Erases the range [first, last]
void clear(); //Erases all of the elements, but the buffer area is kept
```

##### 4. Accessing Elements in Vector

Methods front() and back() return the first and the last element in the vector respectively. The subscript operator can access the elements via the position directly.

#### c) Application

Example 10.1: Find all primes between 2 – N.

We use a vector to rewrite the program in Example 9.4 and here is the program:

```
//10_1.cpp
#include <iostream>
#include <iomanip>
#include <vector> //include the header of vector
using namespace std;
int main() {
    vector<int> A(10); //used to store prime numbers,
                   //initialized with 10 elements
    int n; //upper limit for the numbers,
           //inputted by user
    int primecount = 0, i, j;
    cout << "Enter a value >= 2 as upper limit for prime numbers: ";
    cin >> n;
    A[primecount++] = 2; //2 is a prime number
    for(i = 3; i < n; i++) {
```
