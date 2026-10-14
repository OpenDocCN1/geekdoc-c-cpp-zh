```
using BinaryTree;
```

Remember, this namespace contains the Tree<TItem> class.

6. After the Main method in the Program class, add a method named InsertIntoTree. This method should be declared as a static void method that takes a Tree<TItem> parameter and a params array of TItem elements called data. The tree parameter should be passed by reference, for reasons that will be described in a later step.

The method definition should look like this:

Click here to view code image

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
    params TItem[] data)
{
}
```

7. The TItem type used for the elements being inserted into the binary tree must implement the IComparable<TItem> interface. Modify the definition of the InsertIntoTree method and add the where clause shown in bold in the following code:

Click here to view code image

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
    params TItem[] data) where TItem :IComparable<TItem>
{
}
```

8. Add to the InsertIntoTree method the statements shown in bold in the example that follows.

These statements iterate through the params list, adding each item to the tree by using the Insert method. If the value specified by the tree parameter is null initially, a new Tree<TItem> is created; this is why the tree parameter is passed by reference.

Click here to view code image

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
params TItem[] data) where TItem : IComparable<TItem>
{
    foreach (TItem datum in data)
    {
        if (tree == null)
        {
            tree = new Tree<TItem>(datum);
        }
        else
        {
            tree.Insert(datum);
        }
    }
}
```