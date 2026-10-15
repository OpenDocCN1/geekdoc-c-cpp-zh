```
public class SimpleStack
{
    private readonly double[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new double[10];

    public int Count => _currentIndex + 1;

    public void Push(double item) => _items[++_currentIndex] = item;

    public double Pop() => _items[_currentIndex--];
}
```

So here in the StackDouble method, let's create a SimpleStack instance and let's add an opening angle bracket to pass the generic type argument to the SimpleStack class. Here, we want to use the SimpleStack class with the type double.

```
public class SimpleStack<TypePlaceholder>
{
    private readonly TypePlaceholder[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new TypePlaceholder[10];

    public int Count => _currentIndex + 1;

    public void Push(TypePlaceholder item) => _items[++_currentIndex] = item;

    public TypePlaceholder Pop() => _items[_currentIndex--];
}
```

Now as you can see, the code in this StackDoubles method does not have any errors. When you hover the Push method, you can see it takes a double.