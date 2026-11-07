+   4. Suppose that `stack` is an object of type `stackType<string>` and the value of `stack.top - 1` is 2. How many elements are in the stack? (3)

+   5. Consider the following statements: (3)

Show what is output by the following segment of code:

```
```cpp
stackType<int> stack;
int num1, num2;

stack.push(12);
stack.push(5);
num1 = stack.top() + 3;
stack.push(num1 + 5);
num2 = stack.top();
stack.push(num1 + num2);
num2 = stack.top();
stack.pop();
stack.push(15);
num1 = stack.top();
stack.pop();
while (!stack.isEmptyStack())
{
    cout << stack.top() << " ";
    stack.pop();
}
cout << endl;
cout << "num1 = " << num1 << endl;
cout << "num2 = " << num2 << endl;
```
```

+   6. Consider the following statements: (3)

Suppose that the input is:

```
```text
31 47 86 39 62 71 15 63
```
```

Show what is output by the following segment of code:

```
```cpp
stackType<int> stack(50);
int num;

cin >> num;

while (cin)
{
    if (!stack.isFullStack())
    {
        if (num % 2 == 0 || num % 3 == 0)
            stack.push(num);
        else if (!stack.isEmptyStack())
        {
            cout << stack.top() << " ";
            stack.pop();
        }
    }
    else
        stack.push(num + 3);
}
```
```