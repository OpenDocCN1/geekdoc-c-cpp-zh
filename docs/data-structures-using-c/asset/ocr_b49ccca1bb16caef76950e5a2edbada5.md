```
cout << "Stack is Empty" << endl;
}
Bool Stack :: IsEmpty()
{
if(top == -1)
return 1;
else
return 0;
}
Bool Stack :: IsFull()
{
if(top == MaxCapacity - 1)
return 1;
else
return 0;
}
int Stack :: CurrSize()
{
return(top + 1);
}
void Stack :: push(const T & Element)
{
if(!IsFull())
cout << "Stack is Full" << endl;
else
Stack[++top] = Element;
}
```

# 3.6 MULTIPLE STACKS

Often, data is represented using several stacks. The _contiguous stack_ (stack using an array) uses separate arrays for more than one stack, if needed. The use of a contiguous stack when more than one stack is needed is not a space-efficient approach, because many locations in the stacks are often left unused. An efficient solution to this problem is to use a single array to store more than one stack. Figure 3.11 shows two stacks using one array.