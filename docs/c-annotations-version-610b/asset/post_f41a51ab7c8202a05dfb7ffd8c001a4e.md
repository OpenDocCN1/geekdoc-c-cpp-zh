
- `void erase(pos)` erases the element pointed to by the iterator `pos`. Other elements possibly having the same values are not erased.
- `void erase(first, beyond)` erases all elements indicated by the iterator range `[first, beyond)`.
- `pair<multiset::iterator, multiset::iterator> equal_range(value)`: this member function returns a pair of iterators, being respectively the return values of `lower_bound` and `upper_bound`, introduced below. The function provides a simple means to determine all elements in the multiset that have the same values.
- `multiset::iterator find(value)`: this member returns an iterator pointing to the first element having the specified value. If the element isn't available, `end` is returned. The iterator could be incremented to visit all elements having the given value until it is either `end`, or the iterator doesn't point to 'value' anymore.
- `... insert()`: this member function normally succeeds and returns a `multiset::iterator` rather than a `pair<multiset::iterator, bool>` as returned with the `set` container. The returned iterator points to the newly added element.

Although the functions `lower_bound` and `upper_bound` act identically in the set and multiset containers, their operation in a multiset deserves some additional attention. With a multiset container `lower_bound` and `upper_bound` produce the same result for non-existing keys: they both return the first element having a key exceeding the provided key.

Here is an example showing the use of various member functions of a multiset:

```cpp
#include <iostream>
#include <set>

using namespace std;

int main()
{
    string
        sa[] =
        {
            "alpha",
            "echo",
            "hotel",
            "mike",
            "romeo"
        };

    multiset<string>
        object(&sa[0], &sa[5]);

    object.insert("echo");
    object.insert("echo");

    multiset<string>::iterator
        it = object.find("echo");

    for (; it != object.end(); ++it)
        cout << *it << " ";
    cout << '\n';

    cout << "Multiset::equal_range(\"ech\")\n";
    pair
    <
        multiset<string>::iterator,
        multiset<string>::iterator
    >
        itpair = object.equal_range("ech");

    if (itpair.first != object.end())
        cout << "lower_bound() points at " << *itpair.first << '\n';
    for (; itpair.first != itpair.second; ++itpair.first)
        cout << *itpair.first << " ";

    cout << '\n' <<
        object.count("ech") << " occurrences of 'ech'" << '\n';

    cout << "Multiset::equal_range(\"echo\")\n";
    itpair = object.equal_range("echo");

    for (; itpair.first != itpair.second; ++itpair.first)
        cout << *itpair.first << " ";

    cout << '\n' <<
        object.count("echo") << " occurrences of 'echo'" << '\n';

    cout << "Multiset::equal_range(\"echoo\")\n";
    itpair = object.equal_range("echoo");

    for (; itpair.first != itpair.second; ++itpair.first)
        cout << *itpair.first << " ";

    cout << '\n' <<
        object.count("echoo") << " occurrences of 'echoo'" << '\n';
}

/*
Generated output:

echo echo echo hotel mike romeo
Multiset::equal_range("ech")
lower_bound() points at echo

0 occurrences of 'ech'
Multiset::equal_range("echo")
echo echo echo
3 occurrences of 'echo'
Multiset::equal_range("echoo")

0 occurrences of 'echoo'
*/
```

### 12.3.10 The 'stack' container

The stack class implements a stack data structure. Before using stack containers the header file `<stack>` must have been included.

A stack is also called a first in, last out (FILO or LIFO) data structure as the first item to enter the stack is the last item to leave. A stack is an extremely useful data structure in situations where data must temporarily remain available. For example, programs maintain a stack to store local variables of functions: the lifetime of these variables is determined by the time these functions are active, contrary to global (or static local) variables, which live for as long as the program itself lives. Another example is found in calculators using the Reverse Polish Notation (RPN), in which the operands of operators are kept in a stack, where operators pop their operands off the stack and push the results of their work back onto the stack.

![](img/859c398c8f9601f32700b78894504b0a_300_0.png)

Figure 12.5: The contents of a stack while evaluating `3 4 + 2 *`

As an example of the use of a stack, consider figure 12.5, in which the contents of the stack is shown while the expression (`3 4 + 2 *`) is evaluated. In the RPN this expression becomes `3 4 + 2 *`, and figure 12.5 shows the stack contents after each token (i.e., the operands and the operators) is read from the input. Notice that each operand is indeed pushed on the stack, while each operator changes the contents of the stack. The expression is evaluated in five steps. The caret between the tokens in the expressions shown on the first line of figure 12.5 shows what token has just been read. The next line shows the actual stack-contents, and the final line shows the steps for referential purposes. Note that at step 2, two numbers have been pushed on the stack. The first number (3) is now at the bottom of the stack. Next, in step 3, the + operator is read. The operator pops two operands (so that the stack is empty at that moment), calculates their sum, and pushes the resulting value (7) on the stack. Then, in step 4, the number 2 is read, which is dutifully pushed on the stack again. Finally, in step 5 the final operator * is read, which pops the values 2 and 7 from the stack, computes their product, and pushes the result back on the stack. This result (14) could then be popped to be displayed on some medium.

From figure 12.5 we see that a stack has one location (the top) where items can be pushed onto and popped off the stack. This top element is the stack’s only immediately visible element. It may be accessed and modified directly.

Bearing this model of the stack in mind, let’s see what we formally can do with the stack container. For the stack, the following constructors, operators, and member functions are available:

- **Constructors:**
  - A stack may be constructed empty.

    ```cpp
    stack<string> object;
    ```

  - A stack may be initialized using a copy constructor.

    ```cpp
    extern stack<string> container;
    stack<string> object(container);
    ```

- Only the basic set of container operators are supported by the stack.
- The following member functions are available for stacks:
  - `bool empty():` This member returns true if the stack contains no elements.
  - `void push(value):` this member places `value` at the top of the stack, hiding the other elements from view.
  - `void pop():` this member removes the element at the top of the stack. Note that the popped element is *not* returned by this member. Nothing happens if `pop` is used with an empty stack. See section 12.3.3 for a discussion about the reason why `pop` has return type `void`.
  - `size_t size():` this member returns the number of elements in the stack.
  - `Type &top():` this member returns a reference to the stack's top (and only visible) element. It is the responsibility of the programmer to use this member only if the stack is not empty.

The stack does not support iterators or a subscript operator. The only elements that can be accessed is its top element. To empty a stack:

- repeatedly remove its front element;
- assign an empty stack to it;
- have its destructor called (e.g., by ending its lifetime).

### 12.3.11 Unordered containers (‘hash tables’) (C++11)

The C++11 standard officially adds hash tables to the language.

Before using hash table containers the header file `<unordered_map>` must have been included. Variants are hash-based sets and multi-sets. Before using these hash-based set containers the header file `<unordered_set>` must have been included.

As discussed, the map is a sorted data structure. The keys in maps are sorted using the `operator<` of the key's data type. Generally, this is not the fastest way to either store or retrieve data. The main benefit of sorting is that a listing of sorted keys appeals more to humans than an unsorted list. However, a by far faster method to store and retrieve data is to use hashing.

Hashing uses a function (called the *hash function*) to compute an (unsigned) number from the key, which number is thereupon used as an index in the table in which the keys are stored. Retrieval of a key is as simple as computing the hash value of the provided key, and looking in the table at the computed index location: if the key is present, it is stored in the table, and its value can be returned. If it's not present, the key is not stored.

Collisions occur when a computed index position is already occupied by another element. For these situations the abstract containers have solutions available. A simple solution, adopted by the C++11 standard is to use *linear chaining* which uses a linked list to store colliding table elements in.

In the C++11 standard the term *unordered* is used rather than *hash* to avoid name collisions with hash tables developed before the advent of the C++11 standard. Except where *unordered* is required as part of a type name, we'll use the term *hash* as it is the term that is commonly encountered.

Four forms of unordered data structures are supported: `unordered_map`, `unordered_multimap`, `unordered_set`, and `unordered_multiset`.

Below the `unordered_map` container is discussed. The other containers using hashing also use hashing but provide functionality corresponding to, respectively, the `multimap`, `set` and `multiset`.

Concentrating on the `unordered_map`, its constructor needs a key type, a value type, an object computing a hash value for the key, and an object comparing two keys for equality. Predefined hash functions
