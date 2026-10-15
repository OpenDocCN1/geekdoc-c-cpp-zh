```
{
    public class SimpleStack
    {
        private readonly double[] _items;
        private int _currentIndex = -1;

        public SimpleStack()
        {
            _items = new double[10];
        }

        public void Push(double item)
        {
            _items[++_currentIndex] = item;
        }
    }
}
```

Now let's go back to the Program.cs file. Here in the StackDoubles method, let's use the SimpleStackDouble class.

```
public class SimpleStack
{
    private readonly double[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new double[10];

    public void Push(double item) => _items[++_currentIndex] = item;
}
```

Now, as the push method takes a double, these double values are not boxed anymore into an object container. Also down here, you can