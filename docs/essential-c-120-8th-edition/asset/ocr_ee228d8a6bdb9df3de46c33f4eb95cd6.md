# 648 Chapter 12: Generics

Listing 12.21: Needing the Type Parameter to Support an Interface or Exception Thrown

```
public class BinaryTree<T>
{
    public BinaryTree(T item)
    {
        Item = item;
    }

    public T Item { get; set; }
    public Pair<BinaryTree<T>?>? _SubItems;
    {
        get { return _SubItems; }
        set {
            switch (value)
            {
                // Using C# 8.0 Pattern Matching. Switch to
                // checking for null prior to C# 8.0
                // ...
                case
                    First: {Item: IComparable<T>> first,
                    Second: {T second}:
                    if (first.compareTo(second) < 0)
                    {
                        // first is less than second
                    }
                    else
                    {
                        // second is less than or equal to first
                    }
                    break;
                default:
                    throw new InvalidCastException(
                        "$\Unable to sort the items as {typeof(T)} does not support IComparable<T>"$"
                    );
            }
        }
        _SubItems = value;
    }
}
private Pair<BinaryTree<T>?>? _SubItems;
}
```