Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : 
IComparable<TItem>
{
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }
}
```

+   8. Add the following private method shown in bold, called populate, to the TreeEnumerator<TItem> class, immediately after the constructor:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem : 
IComparable<TItem>
{
    ...
    public TreeEnumerator(Tree<TItem> data)
    {
        this.currentData = data;
    }

    private void populate(Queue<TItem> enumQueue, Tree<TItem> tree)
    {
        if (tree.LeftTree is not null)
        {
            populate(enumQueue, tree.LeftTree);
        }
        enumQueue.Enqueue(tree.NodeData);

        if (tree.RightTree is not null)
        {
            populate(enumQueue, tree.RightTree);
        }
    }
}
```