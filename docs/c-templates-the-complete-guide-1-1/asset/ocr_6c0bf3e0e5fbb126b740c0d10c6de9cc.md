Stack<double> dStack;        // stack of doubles
Stack<int> iStack;           // stack of ints
iStack = dStack;             // ERROR: stack types are not compatible

Again, you could change the implementation to parameterize the internal container type:

```
```cpp
template<typename T, typename Cont = std::deque<T>>
class Stack {
private:
    Cont elems;                 // elements

public:
    void push(T const&);        // push element
    void pop();                 // pop element
    T const& top() const;       // return top element
    bool empty() const {        // return whether stack is empty
        return elems.empty();
    }

    // assign stack of elements of type T2
    template<typename T2, typename Cont2>
    Stack(Stack<T2, Cont2> const&);

    // to get access to private members of Stack<T2>
    template<typename T2, typename Cont2>
    friend class Stack;
};
```
```

Thus, the template assignment operator is implemented like this:

```
```cpp
template<typename T, typename Cont>
template<typename T2, typename Cont2>
Stack<T, Cont>&
Stack<T, Cont>::operator=(Stack<T2, Cont2> const& op2)
{
    elems.clear();                    // remove all
    elems.insert(elems.begin(),       // insert at beginning
                 op2.elems.begin(),
                 op2.elems.end());

    return *this;
}
```
```

Remember, for class templates, only those member functions that are called are instantiated. Thus, if you avoid assigning a stack with elements of a different type, you could even use a vector as the internal container:

```
```cpp
// stack for ints using a vector as internal container
Stack<int, std::vector<int> > vStack;

vStack.push(42); vStack.push(7);
std::cout << vStack.top() << '\n';
```
```

Because the assignment operator template isn't necessary, no error message of a missing member function push_front() occurs and the program is fine.

For the complete implementation of the last example, see the file with a name that starts with v in the subdirectory basic.