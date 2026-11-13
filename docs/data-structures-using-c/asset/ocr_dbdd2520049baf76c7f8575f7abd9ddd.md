# PROGRAM CODE 3.2

```
```cpp
class Stack
{
 private:
 int Stack[50];
 int MaxCapacity;
 int top;
 public:
 Stack()
 {
 MaxCapacity = 50;
 top = -1;
 }
 int getTop();
 int pop();
 void push(int Element);
 int Empty();
 int CurrSize();
 int IsFull();
 };
 int Stack :: getTop()
 {
 if(!Empty())
 return(Stack[top]);
 }
 int Stack :: pop()
 {
 if(!Empty())
 return(Stack[top--]);
 }
 int Stack :: Empty()
 {
 if(top == -1)
 return 1;
 else
 return 0;
 }
```
```