By defining an assignment operator as a template, however, you can enable the assignment of stacks with elements for which an appropriate type conversion is defined. To do this you have to declare `Stack<>` as follows: [Click here to view code image](#)

# basics/stack5decl.hpp

```
template<typename T>
class Stack {
private:
std::deque<T> elems; // elements

public:
void push(T const&); // push element
void pop(); // pop element
T const& top() const; // return top element
bool empty() const { // return whether the stack is empty
return elems.empty();
}

// assign stack of elements of type T2
template<typename T2>
Stack& operator= (Stack<T2> const&);
};
```

The following two changes have been made: 1. We added a declaration of an assignment operator for stacks of elements of another type T2. 2. The stack now uses a `std::deque<>` as an internal container for the elements. Again, this is a consequence of the implementation of the new assignment operator.

The implementation of the new assignment operator looks like this:³

[Click here to view code image](#)

# basics/stack5assign.hpp

```
template<typename T>
template<typename T2>
Stack<T>& Stack<T>::operator= (Stack<T2> const& op2)
{
Stack<T2> tmp(op2); // create a copy of the assigned stack

elems.clear(); // remove existing elements
while (!tmp.empty()) { // copy all elements
elems.push_front(tmp.top());
tmp.pop();
}
return *this;
}
```