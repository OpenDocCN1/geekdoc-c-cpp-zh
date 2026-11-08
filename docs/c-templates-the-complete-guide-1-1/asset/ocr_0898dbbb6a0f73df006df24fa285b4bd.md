```
```cpp
template<>
class Stack<std::string> {
 private:
   std::deque<std::string> elems; // elements

 public:
   void push(std::string const& elem); // push element
   void pop();                        // pop element
   std::string const& top() const;    // return top element
   bool empty() const {               // return whether stack is empty
      return elems.empty();
   }
};

void Stack<std::string>::push(std::string const& elem)
{
   elems.push_back(elem);             // append copy of passed element
}

void Stack<std::string>::pop()
{
   assert(!elems.empty());
   elems.pop_back();                  // remove last element
}

std::string const& Stack<std::string>::top() const
{
   assert(!elems.empty());
   return elems.back();               // return copy of last element
}
```
```

In this example, the specialization uses reference semantics to pass the string argument to `push()`, which makes more sense for this specific type (we should even better pass a forwarding reference, though, which is discussed in Section 6.1 on page 91).

Another difference is due to a unique instead of a vector to manage the elements inside the stack. Although this has no particular benefit here, it does demonstrate that the implementation of a specialization might look very different from the implementation of the primary template.

# 2.6 PARTIAL SPECIALIZATION

Class templates can be partially specialized. You can provide special implementations for particular circumstances, but some template parameters must still be defined by the user. For example, we can define a partial specialization of class `Stack<>` for pointers:

[Click here to view code image](#)

`basics2/src/stackpartial.hpp`

```
```cpp
#include "stack1.hpp"

// partial specialization of class Stack<> for pointers

template<typename T>
class Stack<T*> {
 private:
   std::vector<T*> elems;       // pointers

 public:
   void push(T*);               // push element
   T* pop();                    // pop element
```
```