```
```cpp
//Use the assignment operator to copy the elements
//of stack into otherStack
otherStack = stack;

cout << "Testing the copy constructor." << endl;

testCopy(otherStack);

cout << "After the copy constructor, otherStack: " << endl;

while (!otherStack.isEmptyStack())
{
    cout << otherStack.top() << endl;
    otherStack.pop();
}
return 0;
}

//Function to test the copy constructor
void testCopy(const linkedStackType<int> OStack)
{
    cout << "Stack in the function testCopy:" << endl;

    while (!OStack.isEmptyStack())
    {
        cout << OStack.top() << endl;
        OStack.pop();
    }
}
```
```

# Sample Run:

```
```text
After the assignment operator, newStack:
37
94
28
Testing the copy constructor.
Stack in the function testCopy:
37
94
28
After the copy constructor, otherStack:
37
94
28
```
```