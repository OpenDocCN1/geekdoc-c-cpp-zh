# DISPLAY 18.8  Stack Template Class *(part 2 of 2)*

# Sample Member Functions

| Member Function<br>(s is a Stack Object) | Meaning |
|---|---|
| `s.size()` | Returns the number of elements in the stack. |
| `s.empty()` | Returns *true* if the stack is empty; otherwise returns *false*. |
| `s.top()` | Returns a mutable reference to the top member of the stack. |
| `s.push(Element)` | Inserts a copy of *Element* at the top of the stack. |
| `s.pop()` | Removes the top element of the stack. Note that pop is a void function. It does not return the element removed. |
| `s1 == s2` | True if `s1.size() == s2.size()` and each element of `s1` is equal to the corresponding element of `s2`; otherwise returns *false*. |

The stack template class also has a default constructor, a copy constructor, as well as a constructor that takes an object of any sequential container class and initializes the stack to the elements in the sequence. It also has a destructor that returns all storage for recycling and a well-behaved assignment operator.

# DISPLAY 18.9  Queue Template Class *(part 1 of 2)*

**Queue Adapter Template Class Details**

Type name `queue<T>` or `queue<T, Underlying_Container>` for a queue of elements of type T.
For efficiency reasons, the Underlying_Container cannot be a vector type.
Library header: `<queue>` which places the definition in the std namespace.
Defined types: `value_type`, `size_type`.
There are no iterators.

# Sample Member Functions

| Member Function<br>(q is a Queue Object) | Meaning |
|---|---|
| `q.size()` | Returns the number of elements in the queue. |
| `q.empty()` | Returns *true* if the queue is empty; otherwise returns *false*. |