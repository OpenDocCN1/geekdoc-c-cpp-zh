```
```cpp
// push an element onto the Stack
void push( const T &pushValue )
{
    stack.push_front( pushValue );
} // end function template push

// pop an element from the stack
void pop()
{
    stack.pop_front();
} // end function template pop

// determine whether Stack is empty
bool isEmpty() const
{
    return stack.empty();
} // end function template isEmpty

// return size of Stack
size_t size() const
{
    return stack.size();
} // end function template size

private:
    std::deque< T > stack; // internal representation of the Stack
}; // end class template Stack

#endif
```
```

Fig. 23.1 | Stack class template. (Part 2 of 2.)

# Class Template Stack<T>'s Data Representation

The C++ Standard Library's prepackaged stack adapter class can use various containers to store its elements. Of course, a stack requires insertions and deletions only at its top. So, for example, a vector or a deque could be used to store the stack's elements. A vector supports fast insertions and deletions at its back. A deque supports fast insertions and deletions at its front and its back. A deque is the default representation for the Standard Library's stack adapter because a deque grows more efficiently than a vector. A vector is maintained as a contiguous block of memory—when that block is full and a new element is added, the vector allocates a larger contiguous block of memory and copies the old elements into that new block. A deque, on the other hand, is typically implemented as list of fixed-size, built-in arrays—new fixed-size built-in arrays are added as necessary and none of the existing elements are copied when new items are added to the front or back. For these reasons, we use a deque (line 42) as the underlying container for our Stack class.

# Class Template Stack<T>'s Member Functions

The member-function definitions of a class template are function templates, but are not preceded with the template keyword and template parameters in angle brackets (< and >) when they're defined within the class template's body. As you can see, however, they do