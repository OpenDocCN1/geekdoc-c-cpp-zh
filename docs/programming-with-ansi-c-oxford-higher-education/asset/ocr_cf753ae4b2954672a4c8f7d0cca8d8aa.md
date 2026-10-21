```
```cpp
int GenericSearch(Type TempGenericArray[], Type EleToBeSearched)
{
for(int i = 0; i < 10; i++)
{
if(EleToBeSearched == TempGenericArray[i])
return i;
}
return -1;
}

template <typename ElementType>
class Stack
{
private:
int StackPointer;
ElementType StackArray[10];
public:
Stack()
{
StackPointer = 0;
}
void push(ElementType);
ElementType pop();
};

template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
if(StackPointer > 9)
cout << "Stack overflow! Cannot insert!";
else
StackArray[StackPointer] = value;
StackPointer++;
}

template <typename ElementType>
ElementType Stack <ElementType>::pop()
{
if(StackPointer == 0)
cout << "Stack underflow! Cannot pop";
else
{
StackPointer--;
return StackArray[StackPointer];
}
}

template <>
class Stack <employee>
{
private:
int StackPointer;
int EmpNoArray[10];
public:
Stack()
{
StackPointer = 0;
}
void push(employee);
}
```
```