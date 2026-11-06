
- `void pop_back();` this member removes the last element from the vector. With an empty vector nothing happens.
- `void push_back(value);` this member adds value to the end of the vector.
- `void reserve(size_t request);` if request is less than or equal to capacity, this call has no effect. Otherwise, it is a request to allocate additional memory. If the call is successful, then capacity returns a value of at least request. Otherwise, capacity is unchanged. In either case, size's return value won't change, until a function like resize is called, actually changing the number of accessible elements.
- `void resize();` this member can be used to alter the number of elements that are currently stored in the vector.
  - `resize(n, value)` may be used to resize the vector to a size of n. Value is optional. If the vector is expanded and value is not provided, the additional elements are initialized to the default value of the used data type, otherwise value is used to initialize extra elements.
- `vector::reverse_iterator rbegin();` this member returns an iterator pointing to the last element in the vector.
- `vector::reverse_iterator rend();` this member returns an iterator pointing before the first element in the vector.
- `size_t size();` this member returns the number of elements in the vector.
- `void swap();` this member can be used to swap two vectors using identical data types. Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> v1(7);
    vector<int> v2(10);

    v1.swap(v2);
    cout << v1.size() << " " << v2.size() << '\n';
}
/*
    Produced output:
10 7
*/
```

## 12.3.2 The 'list' container

The list container implements a list data structure. Before using a list container the header file `<list>` must have been included.

The organization of a list is shown in figure 12.1. Figure 12.1 shows that a list consists of separate list-elements, connected by pointers. The list can be traversed in two directions: starting at Front the list may be traversed from left to right, until the 0-pointer is reached at the end of the rightmost list-element. The list can also be traversed from right to left: starting at Back, the list is traversed from right to left, until eventually the 0-pointer emanating from the leftmost list-element is reached.

![](img/859c398c8f9601f32700b78894504b0a_274_0.png)

As a subtlety note the representation given in figure 12.1 is not necessarily used in actual implementations of the list. For example, consider the following little program:

```cpp
int main()
{
    list<int> l;
    cout << "size: " << l.size() << ", first element: " <<
              l.front() << '\n';
}
```

When this program is run it might actually produce the output:

```
size: 0, first element: 0
```

Its front element can even be assigned a value. In this case the implementor has chosen to provide the list with a hidden element. The list actually is a circular list, where the hidden element serves as terminating element, replacing the 0-pointers in figure 12.1. As noted, this is a subtlety, which doesn't affect the conceptual notion of a list as a data structure ending in 0-pointers. Note also that it is well known that various implementations of list-structures are possible (cf. Aho, A.V., Hopcroft J.E. and Ullman, J.D., (1983) Data Structures and Algorithms (Addison-Wesley)).

Both lists and vectors are often appropriate data structures in situations where an unknown number of data elements must be stored. However, there are some rules of thumb to follow when selecting the appropriate data structure.

- When most accesses are random, a vector is the preferred data structure. Example: in a program counting character frequencies in a textfile, a `vector<int> frequencies(256)` is the data structure of choice, as the values of the received characters can be used as indices into the frequencies vector.
- The previous example illustrates a second rule of thumb, also favoring the vector: if the number of elements is known in advance (and does not notably change during the lifetime of the program), the vector is also preferred over the list.
- In cases where insertions or deletions prevail and the data structure is large the list is generally preferred.

At present lists aren't as useful anymore as they used to be (when computers were much slower and more memory-constrained). Except maybe for some rare cases, a vector should be the preferred container; even when implementing algorithms traditionally using lists.

Other considerations related to the choice between lists and vectors should also be given some thought. Although it is true that the vector is able to grow dynamically, the dynamic growth requires data-copying. Clearly, copying a million large data structures takes a considerable amount of time, even on fast computers. On the other hand, inserting a large number of elements in a list doesn't require us to copy non-involved data. Inserting a new element in a list merely requires us to juggle some pointers. In figure 12.2 this is shown: a new element is inserted between the second and third element, creating a new list of four elements. Removing an element from a list is also fairly easy. Starting again from the situation shown in figure 12.1, figure 12.3 shows what happens if element two is removed from our list. Again: only pointers need to be juggled. In this case it's even simpler than adding an element: only two pointers need to be rerouted. To summarize the comparison between lists and vectors: it's probably best to conclude that there is no clear-cut answer to the question what data structure to prefer. There are rules of thumb, which may be adhered to. But if worse comes to worst, a profiler may be required to find out what's best.

![](img/859c398c8f9601f32700b78894504b0a_275_0.png)

![](img/859c398c8f9601f32700b78894504b0a_275_1.png)

The `list` container offers the following constructors, operators, and member functions:

- **Constructors:**
  - A list may be constructed empty:

    As with the vector, it is an error to refer to an element of an empty list.

    ```cpp
    list<string> object;
    ```

  - A list may be initialized to a certain number of elements. By default, if the initialization value is not explicitly mentioned, the default value or default constructor for the actual data type is used. For example:

    ```cpp
    list<string> object(5, string("Hello"));  // initialize to 5 Hello's
    list<string> container(10);                  // and to 10 empty strings
    ```

  - A list may be initialized using a two iterators. To initialize a list with elements 5 until 10 (including the last one) of a `vector<string>` the following construction may be used:

    ```cpp
    extern vector<string> container;
    list<string> object(&container[5], &container[11]);
    ```

  - A list may be initialized using a copy constructor:

    ```cpp
    extern list<string> container;
    list<string> object(container);
    ```

- The list does not offer specialized operators, apart from the standard operators for containers.

- The following member functions are available:
  - `Type &back():` this member returns a reference to the last element in the list. It is the responsibility of the programmer to use this member only if the list is not empty.
  - `list::iterator begin():` this member returns an iterator pointing to the first element in the list, returning end if the list is empty.
  - `void clear():` this member erases all elements from the list.
  - `bool empty():` this member returns true if the list contains no elements.
  - `list::iterator end():` this member returns an iterator pointing beyond the last element in the list.
  - `list::iterator erase():` this member can be used to erase a specific range of elements in the list:
    - `erase(pos)` erases the element pointed to by pos. The iterator `++pos` is returned.
    - `erase(first, beyond)` erases elements indicated by the iterator range [first, beyond). Beyond is returned.
  - `Type &front():` this member returns a reference to the first element in the list. It is the responsibility of the programmer to use this member only if the list is not empty.
  - `... insert():` this member can be used to insert elements into the list. The return value depends on the version of insert that is called:
    - `list::iterator insert(pos)` inserts a default value of type Type at pos, pos is returned.
    - `list::iterator insert(pos, value)` inserts value at pos, pos is returned.
    - `void insert(pos, first, beyond)` inserts the elements in the iterator range [first, beyond).
    - `void insert(pos, n, value)` inserts n elements having value value at position pos.
  - `void merge(list<Type> other):` this member function assumes that the current and other lists are sorted (see below, the member sort). Based on that assumption, it inserts the elements of other into the current list in such a way that the modified list remains sorted. If both lists are not sorted, the resulting list will be ordered 'as much as possible', given the initial ordering of the elements in the two lists. `list<Type>::merge` uses `Type::operator<` to sort the data in the list, which operator must therefore be available. The next example illustrates the use of the merge member: the list 'object' is not sorted, so the resulting list is ordered 'as much as possible'.

```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

void showlist(list<string> &target)
{
    for
    (
        list<string>::iterator from = target.begin();
        from != target.end();
```
