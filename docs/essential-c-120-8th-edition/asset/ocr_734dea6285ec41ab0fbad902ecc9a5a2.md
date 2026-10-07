# 872 Chapter 17: Building Custom Collections

```
{
    if(tree != null)
    {
      // Since each element in the pair is a tree,
      // traverse the tree and yield each
      // element
      foreach(T item in tree)
      {
        yield return item;
      }
    }
}
#endregion IEnumerable<T>
#region IEnumerable Members
System.Collections.IEnumerable
    System.Collections.IEnumerable.GetEnumerator()
    {
      return GetEnumerator();
    }
#endregion
// ...
```

In Listing 17.17, the first iteration returns the root element within the binary tree. During the second iteration, you traverse the pair of subelements. If the subelement pair contains a non-null value, you traverse into that node and yield its elements. Note that foreach (T item in tree) is a recursive call to a child node.

As observed with CSharpBuiltInTypes and Pair<T>, you can now iterate over BinaryTree<T> using a foreach loop. Listing 17.18 demonstrates this process, and Output 17.6 shows the results.

# LISTING 17.18: Using foreach with BinaryTree<string>

```
// JFK
var jfkFamilyTree = new BinaryTree<string>(
    "John Fitzgerald Kennedy"
{
    SubItems = new Pair<BinaryTree<string>>(
        new BinaryTree<string>("Joseph Patrick Kennedy")
    {
```