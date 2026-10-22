First let’s look at the syntax to define a member template. Inside the template with template parameter T, an inner template with template parameter T2 is defined: [Click here to view code image](#)

```
template<typename T>
template<typename T2>
...
```

Inside the member function, you may expect simply to access all necessary data for the assigned stack op2. However, this stack has a different type (if you instantiate a class template for two different argument types, you get two different class types), so you are restricted to using the public interface. It follows that the only way to access the elements is by calling `top()`. However, each element has to become a top element, then. Thus, a copy of op2 must first be made, so that the elements are taken from that copy by calling `pop()`. Because `top()` returns the last element pushed onto the stack, we might prefer to use a container that supports the insertion of elements at the other end of the collection. For this reason, we use a `std::deque<>`, which provides `push_front()` to put an element on the other side of the collection.

To get access to all the members of op2 you can declare that all other stack instances are friends: [Click here to view code image](#)

# `basics/stack6decl.hpp`

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
// to get access to private members of Stack<T2> for any type T2:
template<typename> friend class Stack;
};
```