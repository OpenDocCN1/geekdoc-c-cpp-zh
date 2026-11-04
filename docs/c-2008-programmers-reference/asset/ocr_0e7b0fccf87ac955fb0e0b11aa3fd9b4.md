```
```csharp
public bool Find(T keyword)
{
    bool found = false;
    for (int i = 0; i < _pointer; i++)
    {
        if (_elements[i].CompareTo(keyword) == 0)
        {
            found = true;
            break;
        }
    }
    return found;
}
```
```

```
```csharp
public bool Empty
{
    get
    {
        return (_pointer <= 0);
    }
}

public static MyStack<T> operator +
    (MyStack<T> stackA, MyStack<T> stackB)
{
    while (!stackB.Empty)
    {
        T item = stackB.Pop();
        stackA.Push(item);
    }
    return stackA;
}
}
```
```

The + operator takes in two operands — the generic *MyStack* objects. Internally, you pop out each element from the second stack and push it into the first stack. The *Empty* property allows you to know if a stack is empty.

To print out the elements of *stack1* after the joining, use the following statements:

```
```csharp
stack1 += stack2;
while (!stack1.Empty)
    Console.WriteLine(stack1.Pop());
```
```

Here’s the output:

```
```
C
D
B
A
```
```