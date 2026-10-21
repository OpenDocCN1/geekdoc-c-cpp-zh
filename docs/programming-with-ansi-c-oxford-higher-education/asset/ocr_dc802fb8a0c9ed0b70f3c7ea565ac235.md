```
```cpp
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
```
```

```
```cpp
template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
if(StackPointer > 9)
{
cout << "Stack overflow! Cannot insert";
}
else
{
StackArray[StackPointer] = value; StackPointer++;
}
}
```
```

```
```cpp
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
```
```

```
```cpp
void main()
{
Stack <int> MyStack;
MyStack.push(1);
MyStack.push(2);
cout << MyStack.pop() << "\n";
cout << MyStack.pop() << "\n";
Stack <char> YourStack;
YourStack.push('n');
YourStack.push('o');
cout << YourStack.pop() << "\n";
cout << YourStack.pop() << "\n";
Stack <employee> EmpStack;
employee UniEmployee[10] = 
{
employee(1, "Lara", "Exam", "Professor"),
employee(2, "Ponting", "Marks heet", "Clerk"),
employee(3, "Laxman", "Accounts", "Head Clerk"),
employee(4, "Flintoff", "Exam", "Clerk")
,
};
```
```