# BEGINNER TOPIC

# struct versus class

An interesting side effect of defining Pair<T> as a struct rather than a class is that SubItems.First and SubItems.Second cannot be assigned directly, even if the setter were public. If you modify the setter to be public, the following will produce a compile error indicating that SubItems cannot be modified, “because it is not a variable”:

```
jfkFamilyTree.SubItems.First =
    new BinaryTree<string>("Joseph Patrick Kennedy");
```

The issue is that SubItems is a property of type Pair<T>, a struct. Therefore, when the property returns the value, a copy of SubItems is made, and assigning First on a copy that is promptly lost at the end of the statement would be misleading. Fortunately, the C# compiler prevents this error.

To overcome the issue, don’t assign First (see the approach in Listing 16.17), use class rather than struct for Pair<T>, don’t create a SubItems property and instead use a field, or provide properties in BinaryTree<T> that give direct access to SubItems members.

# Canceling Further Iteration: yield break

Sometimes you might want to cancel further iteration. You can do so by including an if statement so that no further statements within the code are executed. However, you can also use yield break to cause MoveNext() to return false and control to return immediately to the caller and end the loop. Listing 16.18 shows an example of such a method.

# LISTING 16.18: Escaping Iteration via yield break

```
public System.Collections.Generic.IEnumerable<T>
    GetNotNullEnumerator()
{
    if((First == null) || (Second == null))
    {
        yield break;
    }
    yield return Second;
    yield return First;
}
```

This method cancels the iteration if either of the elements in the Pair<T> class is null.