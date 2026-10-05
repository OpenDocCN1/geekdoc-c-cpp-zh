
## 18.2. CLASS TEMPLATES

```
/*
 * The destructor frees up the memory held by the list
 */
~List() {
  clear(); // Deallocate space held by the list nodes
}

/*
 * insert(elem)
 * Inserts element onto the back of the list.
 * elem is the element to insert.
 */
void insert(const T elem) {
  head = insert(head, elem); // Delegate work to private helper method
}

/*
 * print()
 * Prints the contents of the linked list.
 * Defers the actual work to the private
 * overloaded print method.
 */
void print() const {
  print(head); // Delegate work to private helper method
}

/*
 * Returns the length of the linked list.
 * Defers the actual work to the private
 * overloaded length method.
 */
int length() const {
  return length(head); // Delegate work to private helper method
}

/*
 * clear()
 * Removes all the elements in the linked list.
 * The private dispose function does the hard work.
 */
void clear() {
  dispose(head); // Deallocate space for all the nodes
  head = nullptr; // Null head signifies list is empty
}
```

Notice that in Listing 18.9 (list) the linked elements have the generic type T. Observe carefully that the T parameter appears in the code. Listing 18.10 (templatelistmain.cpp) shows how a client can instantiate the LList template for integer elements. The code in Listing 18.10 (templatelistmain.cpp) contains only trivial changes to just two lines of the code in Listing 16.8 (list.cpp).

## Listing 18.10: templatelistmain.cpp

```cpp
// templatelistmain.cpp
```

## 18. CLASS TEMPLATES

```cpp
#include "llist.h" // Was => #include "intlist.h"
#include <iostream>

using namespace std;

int main() {
    bool done = false;
    char command;
    int value;
    LList<int> list; // Was => IntList list;

    while (!done) {
        cout << "Insert <item> P)rint L)length E)rase Q)uit >>";
        cin >> command;
        switch (command) {
            case 'I': // Insert a new element into the list
            case 'i':
                if (cin >> value)
                    list.insert(value);
                else
                    done = true;
                break;
            case 'P': // Print the contents of the list
            case 'p':
                list.print();
                break;
            case 'L': // Print the list's length
            case 'l':
                cout << "Number of elements: " << list.length() << endl;
                break;
            case 'E': // Erase the list
            case 'e':
                list.clear();
                break;
            case 'Q': // Exit the loop (and the program)
            case 'q':
                done = true;
                break;
        }
    }
}
```

The statement

`LList<int> list;`

instantiates an actual class where all occurrences of T become int. It also declares list to be an object of this instantiated class.

Just as we instantiate function templates with multiple different types within the same program, we can do the same for class templates. The class template LList in Listing 18.9 (llist.h) makes the following client code:

```cpp
LList<int> intlist;
LList<string> strlist;
```

## 18.3. ITERATORS

```cpp
intlist.insert(5);
strlist.insert("Wow");
intlist.print();
strlist.print();
```

This code fragment simultaneously manages lists of integers and lists of string objects.

By now you have probably doubted the fact that `std::vector` is a class template. The **vector** class template is much more sophisticated than our simple `LList` template, but the basic mechanism for its design, a class template, is the same.

11.2 and the extended information in Appendix F demonstrate how we can use a pointer to access the elements within an array. A vector is an object that manages a primitive array, and the developers of the class designed vectors to look and feel as much as possible as arrays. They adopted the square bracket `[]` operator to access elements. They also devised for programmers to use pointer-like objects to access the elements within a vector. These pointer-like objects are called *iterators*.

An iterator is an object that allows to traverse and access elements of a data structure in implementation independent way. C++ provides two global functions, **begin** and **end**, that produce iterators to move forward and back.

In order to behave like a pointer, an iterator provides the following methods:

- `operator*`: to access the element at the current position.
- `operator++`: to move to the next element.
- `operator==`: to determine whether two iterator refer to the same element.

Listing 18.11 (simpleiterator.cpp) shows how to use these methods.

## Listing 18.11: simpleiterator.cpp

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // Make a simple vector
    vector<int> vec = {10, 20, 30, 40, 50};
    // Initialize an iterator to the first element
    vector<int>::iterator iter = vec.begin();
    // Print the elements
    while (iter != vec.end()) {
        cout << *iter << " ";
        iter++;
    }
    cout << endl;
    return 0;
}
```
