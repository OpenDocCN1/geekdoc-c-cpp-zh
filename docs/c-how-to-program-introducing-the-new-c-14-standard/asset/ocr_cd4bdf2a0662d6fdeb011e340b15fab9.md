`isStackEmpty` calls `isEmpty` (line 23) and `printStack` calls `print` (line 28)—this is referred to as **delegation**.

```
```cpp
// Fig. 19.13: Stack.h
// Stack class-template definition.
#ifndef STACK_H
#define STACK_H

#include "List.h" // List class definition

template<typename STACKTYPE>
class Stack : private List<STACKTYPE> {
public:
   // push calls the List function insertAtFront
   void push(STACKTYPE& data) {
      insertAtFront(data);
   }

   // pop calls the List function removeFromFront
   bool pop(STACKTYPE& data) {
      return removeFromFront(data);
   }

   // isStackEmpty calls the List function isEmpty
   bool isStackEmpty() const {
      return this->isEmpty();
   }

   // printStack calls the List function print
   void printStack() const {
      this->print();
   }
};

#endif
```
```

**Fig. 19.13** `Stack` class-template definition.