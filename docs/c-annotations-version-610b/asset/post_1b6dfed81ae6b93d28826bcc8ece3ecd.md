
## 12.3 SEQUENTIAL CONTAINERS

```cpp
#include <string>
#include <queue>
using namespace std;

int main()
{
    priority_queue<string> q;
    string word;

    while (cin >> word)
        q.push(word);

    while (q.size())
    {
        cout << q.top() << " \n";
        q.pop();
    }
}
```

Unfortunately, the words are listed in reversed order: because of the underlying `operator<` the words appearing later in the ASCII-sequence appear first in the priority queue. A solution to that problem is to define a wrapper class around the `string` datatype, reversing `string`’s `operator<`. Here is the modified program:

```cpp
#include <iostream>
#include <string>
#include <queue>

class Text
{
    std::string d_s;

public:
    Text(std::string const &str)
        :
            d_s(str)
        {}
    operator std::string const & () const
    {
        return d_s;
    }
    bool operator<(Text const &right) const
    {
        return d_s > right.d_s;
    }
};

using namespace std;

int main()
{
    priority_queue<Text> q;
    string word;

    while (cin >> word)
        q.push(word);

    while (q.size())
    {
        word = q.top();
        cout << word << '\n';
        q.pop();
    }
}
```

Other possibilities to achieve the same exist. One would be to store the contents of the priority queue in, e.g., a vector, from which the elements can be read in reversed order.

The following constructors, operators, and member functions are available for the `priority_queue` container:

- **Constructors:**
  - A `priority_queue` may be constructed empty:

    ```cpp
    priority_queue<string> object;
    ```

    As with the vector, it is an error to refer to an element of an empty priority queue.
  - A priority queue may be initialized using a copy constructor:

    ```cpp
    extern priority_queue<string> container;
    priority_queue<string> object(container);
    ```

- The `priority_queue` only supports the basic operators of containers.
- The following member functions are available for priority queues:
  - `bool empty();`

    This member returns true if the priority queue contains no elements.
  - `void push(value);`

    This member inserts value at the appropriate position in the priority queue.
  - `void pop();`

    This member removes the element at the top of the priority queue. Note that the element is *not* returned by this member. Nothing happens if this member is called for an empty priority queue. See section 12.3.3 for a discussion about the reason why pop has return type `void`.
  - `size_t size();`

    This member returns the number of elements in the priority queue.
  - `Type &top();`

    This member returns a reference to the first element of the priority queue. It is the responsibility of the programmer to use the member only if the priority queue is not empty.

Note that the priority queue does not support iterators or a subscript operator. The only element that can be accessed is its top element. A priority queue can be emptied by:

- repeatedly removing its top element;
- assigning an empty queue using the same data type to it;
- having its destructor called.

### 12.3.5 The ‘deque’ container

The deque (pronounce: ‘deck’) class implements a doubly ended queue data structure (deque). Before using a deque container the header file `<deque>` must have been included.

A deque is comparable to a queue, but it allows for reading and writing at both ends. Actually, the deque data type supports a lot more functionality than the queue, as illustrated by the following overview of available member functions. A deque is a combination of a vector and two queues, operating at both ends of the vector. In situations where random insertions and the addition and/or removal of elements at one or both sides of the vector occurs frequently using a deque should be considered.

The following constructors, operators, and member functions are available for deques:

- **Constructors:**
  - A deque may be constructed empty:

    ```cpp
    deque<string> object;
    ```

    As with the vector, it is an error to refer to an element of an empty deque.
  - A deque may be initialized to a certain number of elements. By default, if the initialization value is not explicitly mentioned, the default value or default constructor for the actual data type is used. For example:

    ```cpp
    deque<string> object(5, string("Hello"));   // initialize to 5 Hello’s
    deque<string> container(10);                 // and to 10 empty strings
    ```

  - A deque may be initialized using two iterators. To initialize a deque with elements 5 until 10 (including the last one) of a `vector<string>` the following construction may be used:

    ```cpp
    extern vector<string> container;
    deque<string> object(&container[5], &container[11]);
    ```

  - A deque may be initialized using a copy constructor:

    ```cpp
    extern deque<string> container;
    deque<string> object(container);
    ```

- In addition to the standard operators for containers, the deque supports the index operator, which may be used to retrieve or reassign random elements of the deque. Note that the indexed elements must exist.

- The following member functions are available for deques:
  - `Type &back();`

    This member returns a reference to the last element in the deque. It is the responsibility of the programmer to use the member only if the deque is not empty.
  - `deque::iterator begin();`

    This member returns an iterator pointing to the first element in the deque.
  - `void clear();`

    This member erases all elements in the deque.
  - `bool empty();`

    This member returns true if the deque contains no elements.
  - `deque::iterator end();`

    This member returns an iterator pointing beyond the last element in the deque.
  - `deque::iterator erase();`

    The member can be used to erase a specific range of elements in the deque:

    - `erase(pos)` erases the element pointed to by `pos`. The iterator `++pos` is returned.
    - `erase(first, beyond)` erases elements indicated by the iterator range `[first, beyond)`. Beyond is returned.
  - `Type &front();`

    This member returns a reference to the first element in the deque. It is the responsibility of the programmer to use the member only if the deque is not empty.
  - `... insert();`

    This member can be used to insert elements starting at a certain position. The return value depends on the version of insert that is called:

    - `deque::iterator insert(pos)` inserts a default value of type `Type` at `pos`, `pos` is returned.
    - `deque::iterator insert(pos, value)` inserts `value` at `pos`, `pos` is returned.
    - `void insert(pos, first, beyond)` inserts the elements in the iterator range `[first, beyond)`.
    - `void insert(pos, n, value)` inserts `n` elements having value `value` starting at iterator position `pos`.
  - `void pop_back();`

    This member removes the last element from the deque. With an empty deque nothing happens.
  - `void pop_front();`

    This member removes the first element from the deque. With an empty deque nothing happens.
  - `void push_back(value);`

    This member adds value to the end of the deque.
  - `void push_front(value);`

    This member adds value before the first element of the deque.
  - `void resize();`

    This member can be used to alter the number of elements that are currently stored in the deque:

    - `resize(n, value)` may be used to resize the deque to a size of `n`. `value` is optional. If the deque is expanded and `value` is not provided, the additional elements are initialized to the default value of the used data type, otherwise `value` is used to initialize extra elements.
  - `deque::reverse_iterator rbegin();`

    This member returns an iterator pointing to the last element in the deque.
  - `deque::reverse_iterator rend();`

    This member returns an iterator pointing before the first element in the deque.
  - `size_t size();`

    This member returns the number of elements in the deque.
  - `void swap(argument);`

    This member can be used to swap two deques using identical data types.

### 12.3.6 The ‘map’ container

The map class offers a (sorted) associative array. Before using a map container the `<map>` header file must have been included.

A map is filled with key/value pairs, which may be of any container-accepted type. Since types are associated with both the key and the value, we must specify two types in the angle bracket notation, comparable to the specification we’ve seen with the pair container (cf. section 12.2). The first type represents the key’s type, the second type represents the value’s type. For example, a map in which the key is a string and the value is a double can be defined as follows:

```cpp
map<string, double> object;
```
