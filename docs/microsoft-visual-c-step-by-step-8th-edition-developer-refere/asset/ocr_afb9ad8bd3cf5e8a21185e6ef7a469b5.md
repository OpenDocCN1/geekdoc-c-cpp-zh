```
IComparable<TItem>
{
}
```

5. Add to the TreeEnumerator<TItem> class the following three private variables, shown in the following code in bold:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    private Tree<TItem> currentData = null;
    private TItem currentItem = default(TItem);
    private Queue<TItem> enumData = null;
}
```

The currentData variable will be used to hold a reference to the tree being enumerated, and the currentItem variable will hold the value returned by the Current property. You will populate the enumData queue with the values extracted from the nodes in the tree, and the MoveNext method will return each item from this queue in turn. The default keyword is explained in the section “Initializing a variable defined with a type parameter” later in this chapter.

6. Add a constructor that takes a Tree<TItem> parameter called data to the TreeEnumerator<TItem> class. In the body of the constructor, add a statement that initializes the currentData variable to data:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }
}
```

7. Add the following private method, called populate, to the TreeEnumerator<TItem> class, immediately after the constructor:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : IComparable<TItem>
{
    ...
    private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
    {
        if (tree.LeftTree != null)
        {
```