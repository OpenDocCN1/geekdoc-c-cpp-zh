The `default` keyword returns `null` for reference types (that is, if `T` is a reference type) and `0` for numeric types. If the type is a `struct`, it will return each member of the `struct` initialized to `0` (for numeric types) or `null` (for reference types).

# ## Advantages of Generics

It’s not difficult to see the advantages of using generics:

+   - **Type safety** — Generic types enforce type compliance at compile time, not at runtime (as in the case of using `Object`). This reduces the chances of data-type conflict during runtime.
+   - **Performance** — The data types to be used in a generic class are determined at compile time, so there’s no need to perform type casting during runtime, which is a computationally costly process.
+   - **Code reuse** — Because you need to write the class only once and then customize it for use with the various data types, there is a substantial amount of code reuse.

# ## Using Constraints in a Generic Type

Using the MyStack class, suppose that you want to add a method called Find() that allows users to check if the stack contains a specific item. You implement the Find() method like this:

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
            return default(T);
            //throw new Exception("Stack is empty.");
        }
    }
}
```
```