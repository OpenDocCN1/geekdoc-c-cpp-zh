# # Using the default Keyword in Generics

In the preceding implementation of the generic MyStack class, the Pop() method throws an exception whenever you call it when the stack is empty:

```
```csharp
public T Pop()
{
    _pointer--;
    if (_pointer < 0)
    {
        throw new Exception("Stack is empty.");
    }
    return _elements[_pointer];
}
```
```

Rather than throwing an exception, you might want to return the default value of the type used in the class. If the stack is dealing with int values, it should return 0; if the stack is dealing with string, it should return an empty string. In this case, you can use the default keyword to return the default value of a type:

```
```csharp
public T Pop()
{
    _pointer--;
    if (_pointer < 0)
    {
        return default(T);
    }
    return _elements[_pointer];
}
```
```

For instance, if the stack deals with int values, calling the Pop() method on an empty stack will return 0:

```
```csharp
MyStack<int> stack = new MyStack<int>(3);
stack.Push(1);
stack.Push(2);
stack.Push(3);

Console.WriteLine(stack.Pop()); //---3---
Console.WriteLine(stack.Pop()); //---2---
Console.WriteLine(stack.Pop()); //---1---
Console.WriteLine(stack.Pop()); //---0---
```
```

Likewise, if the stack deals with the string type, calling Pop() on an empty stack will return an empty string:

```
```csharp
MyStack<string> stack = new MyStack<string>(3);
stack.Push("A");
stack.Push("B");
stack.Push("C");

Console.WriteLine(stack.Pop()); //---"C"---
Console.WriteLine(stack.Pop()); //---"B"---
Console.WriteLine(stack.Pop()); //---"A"---
Console.WriteLine(stack.Pop()); //---""---
```
```