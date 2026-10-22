basics/stackpartspec.hpp

```
#include "stack1.hpp"

// partial specialization of class Stack<> for pointers:
template<typename T>
class Stack<T*> {
    private:
        std::vector<T*> elems;      // elements

    public:
        void push(T*);              // push element
        T* pop();                   // pop element
        T* top() const;             // return top element
        bool empty() const {        // return whether the stack is empty
            return elems.empty();
        }
}
```