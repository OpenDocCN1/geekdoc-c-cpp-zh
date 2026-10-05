
There are a number of predefined function objects declared in <functional>. These are:

| plus | minus | multiplies | divides | modulus |
| :--- | :--- | :--- | :--- | :--- |
| negate | equal_to | not_equal_to | greater | greater_equal |
| less | less_equal | logical_and | logical_or | logical_not |

Using function objects rather than function pointers allows the STL to generate efficient code.

The STL also uses binders and negators. A binder binds an argument to a function object. A negator returns the complement of a predicate.

The STL also implements adaptors. An adaptor transforms one thing into another. For example, the queue container is an adaptor for the deque container.

## The Container Classes

Containers are STL objects that store other objects. The STL defines the following containers:

| Container | Description | Required Header |
| :--- | :--- | :--- |
| bitset | A set of bits. | <bitset> |
| deque | A double-ended queue. | <deque> |
| list | A linear list. | <list> |
| map | Stores key/value pairs. Each key is associated with only one value. | <map> |
| multimap | Stores key/value pairs in which one key may be associated with two or more values. | <map> |
| multiset | A set in which each element is not necessarily unique. | <set> |
| priority_queue | A priority queue. | <queue> |
| queue | A queue. | <queue> |
| set | A set in which each element is unique. | <set> |
| stack | A stack. | <stack> |
| vector | A dynamic array. | <vector> |

## General Theory Of Operation

Firstly, we must decide on the type of container that we want to use. Each container type offers certain benefits and trade-offs. For example, a vector is a very good choice when a random-access, array-like object is required and not too many insertions or deletions will occur. A list has low-cost insertions and deletions but slower access speed than a vector.

Once we have chosen a container, we can use its member functions to add elements to the container, access and modify elements, and delete elements.

Except for the bitset container, a container will automatically grow as needed when elements are added to it and shrink when elements are removed.

A common way to access elements within a container is through an iterator. The sequence and associative containers implement the member functions begin and end, which return iterators to the start and end of a container. These iterators are very useful for accessing the contents of a container. For example, in order to cycle through the elements of a container, we obtain an iterator to its beginning using the begin() function and then increment the iterator until its value is equal to end().

**Important Note:** In general, STL containers will not accept variables or reference parameters in template declarations.

## Vector Containers

A vector is a dynamic array. This is an array that can automatically grow or shrink as needed. In C++, the size of an array is fixed at compile time. While this is by far the most efficient way to implement arrays, it is also the most restrictive because the size of the array cannot be varied at run-time to accommodate changing program conditions. A vector container solves this problem by automatically allocating memory for the array, as needed.

The template declaration for a vector is:

```cpp
template <class T, class Allocator = allocator<T>> class vector {};
```

T is the type of data to be stored in the vector. *Allocator* specifies the memory allocator, this defaults to the standard allocator.

A vector container has the following constructors:

```cpp
explicit vector(const Allocator &a = Allocator() );
```

This constructor creates an empty vector.

The **explicit** keyword prevents any implicit type conversions from occurring. The = sign indicates a default template parameter value.

The second constructor makes a vector that has num elements each with the value val.

```cpp
explicit vector(size_t num, const T& val,
    const Allocator &a = Allocator());
```

The third constructor makes a vector that contains the same elements as a second vector.

```cpp
vector(const vector<T, Allocator>& second_vector);
```

The fourth constructor makes a vector that contains elements in the range specified by the iterators start and end:

```cpp
vector(Iterator_t start, Iterator_t end, const Allocator &a =
Allocator());
```

Any object that will be stored in a vector must have a constructor. It must also define the == operators. Some compilers may require other comparison operators be defined. All of built-in C++ types automatically satisfy these requirements. Although vector syntax looks complex, declaring a vector is easy. Here are some examples:

- create a zero length integer vector: `vector<int> iv;`
- create a five element char vector: `vector<char> cv(5);`
- create a five character vector initialized with 'x': `vector<char> cv(5, 'x');`
- create a vector from dv integer type: `vector<int> dv(dv);`

STL defines the following operators for vectors: ==, <, <=, !=, >=. The index operator [] implements random access to the elements of a vector.

The Vector container has numerous member functions. The size function returns the current size. The begin function returns an iterator to the start of the vector. The end function returns an iterator to the end of the vector. The push_back function pushes a value onto the end of a vector. If necessary, the vector is increased in length to accommodate the new element. pop_back removes the last element of the vector. insert inserts an element at a specified position in the vector. We can remove all the elements in a vector with clear(). empty() is a predicate that tests if a vector is empty.

The following example demonstrates a vector:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main ()
{
    // create integer vector of length 10
    vector<int> v(10);
    size_t i;

    // display the size
    cout << "Size = " << v.size() << endl;

    // assign values to the elements of the vector
    for (i = 0; i < 10; i++) v[i] = i;

    // display contents of the vector
    cout << "Current Contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // push more values onto the end of the vector,
    // the vector will grow as needed
    for (i = 0; i < 5; i++) v.push_back(i + 10);

    // display the current size of v
    cout << "Vector size now = " << v.size() << endl;

    // display contents of the vector
    cout << "Current contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // change the contents of the vector
    for (i = 0; i < v.size(); i++) v[i] = v[i] + 100;

    cout << "Modified vector contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << endl;

    return 0;
}

// output
size = 10
Current Contents:
0 1 2 3 4 5 6 7 8 9
Vector size now = 15
Current contents:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
Modified vector contents:
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114
```

## Accessing a Vector Through an Iterator

Arrays and pointers are closely related in C and C++. An array element can be accessed either through its index or through a pointer. We also access the data members of a vector with an index or through the use of an iterator:

```cpp
// Access the elements of a vector through an iterator
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v(10); // create an int vector of length 10
    // create an iterator to a (generic) int vector
    vector<int>::iterator p = v.begin();

    size_t i;

    // get the iterator to the first element of v
    p = v.begin();
    i = 0;

    // assign values to elements in vector v
    while (p != v.end()) {
        *p = i;
        p++;
        i++;
    }

    // display contents of vector v
    cout << "Original vector contents:\n";
    p = v.begin();
    while (p != v.end()) {
        cout << *p << " ";
    }
    cout << "\n";

    // change the contents of vector v
    p = v.begin();
    while (p != v.end()) {
        *p = *p + 100;
        p++;
    }

    // iterate through the contents of the changed vector
    cout << "Modified vector contents:\n";
    p = v.begin();
    while (p != v.end()) {
        cout << *p << " ";
    }
    cout << endl;

    return 0;
}

// output
Original vector contents:
0 1 2 3 4 5 6 7 8 9

Modified vector contents:
100 101 102 103 104 105 106 107 108 109
```
