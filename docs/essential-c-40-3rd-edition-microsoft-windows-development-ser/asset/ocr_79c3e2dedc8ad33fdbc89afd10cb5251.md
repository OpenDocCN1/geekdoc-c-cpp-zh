```
{
    IComparable first;
    first = (IComparable)value.First.Value;

    if (first.CompareTo(value.Second.Value) < 0)
    {
        // first is less than second.
    }
    else
    {
        // first and second are the same or
        // second is less than first.
    }
    _SubItems = value;
}

private Pair<BinaryTree<T>> _SubItems;

public T this[params PairItem[] branches]
{
    get
    {
        BinaryTree<T> currentNode = this;
        int totallevels =
            (branches == null) ? 0 : branches.Length;
        int currentlevel = 0;

        while (currentlevel < totallevels)
        {
            currentNode =
                currentNode._SubItems[branches[currentlevel]];

            if (currentNode == null)
            {
                // The binary tree at this Location is null.
                throw new IndexOutOfRangeException();
            }

            currentlevel++;
        }

        return currentNode.Value;
    }
}
#region IEnumerable<T>
// Listing 12.22
public IEnumerator<T> GetEnumerator()
{
    // Return the item at this node.
    yield return Value;

    // Iterate through each of the elements in the pair.
```