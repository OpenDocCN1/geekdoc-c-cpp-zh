# Generic Classes

Using generics, you do not need to fix the data type of the items used by your stack class. Instead, you use a generic type parameter (<T>) that identifies the data type parameter on a class, structure, interface, delegate, or procedure. Here's a rewrite of the MyStack class that shows the use of generics:

```
```csharp
public class MyStack<T>
{
    private T[] _elements;
    private int _pointer;
    public MyStack(int size)
    {
        _elements = new T[size];
        _pointer = 0;
    }
    public void Push(T item)
    {
        if (_pointer > _elements.Length - 1)
        {
            throw new Exception("Stack is full.");
        }
        _elements[_pointer] = item;
        _pointer++;
    }
    public T Pop()
    {
        _pointer--;
        if (_pointer < 0)
        {
            throw new Exception("Stack is empty.");
        }
        return _elements[_pointer];
    }
}
```
```

As highlighted, you use the type T as a placeholder for the eventual data type that you want to use for the class. In other words, during the design stage of this class, you do not specify the actual data type that the MyStack class will deal with. The MyStack class is now known as a generic type.

When declaring the private member array _element, you use the generic parameter T instead of a specific type such as int or string:

```
```csharp
private T[] _elements;
```
```

In short, you replace all specific data types with the generic parameter T.

> You can use any variable name you want to represent the generic parameter. T is chosen as the generic parameter for illustration purposes.