# Iterators 871

will always work because of the type compatibility (via inheritance) between IEnumerable<T> and IEnumerable. Since the signatures for both versions of GetEnumerator() are identical (the return type does not distinguish a signature), one or both implementations must be explicit. Given the additional type safety offered by IEnumerable<T> version, you implement IEnumerable's implementation explicitly.

Listing 17.16 uses the Pair<T>.GetEnumerator() method and displays "Inigo" and "Montoya" on two consecutive lines.

# LISTING 17.16: Using Pair<T>.GetEnumerator() via foreach

```
var fullName = new Pair<string>("Inigo", "Montoya");
foreach(string name in fullName)
{
    Console.WriteLine(name);
}
```

Notice that the call to GetEnumerator() is implicit within the foreach loop.

# Placing a yield return within a Loop

It is not necessary to hardcode each yield return statement, as you did in CSharpBuiltInTypes and Pair<T>. Using the yield return statement, you can return values from inside a loop construct. Listing 17.17 uses a foreach loop. Each time the foreach within GetEnumerator() executes, it returns the next value.

# LISTING 17.17: Placing yield return Statements within a Loop

```
public class BinaryTree<T> :
    IEnumerable<T>
{
    // ...
    #region IEnumerable<T>
    public IEnumerable<T> GetEnumerator()
    {
        // Return the item at this node
        yield return Value;

        // Iterate through each of the elements in the pair
        foreach (BinaryTree<T>? tree in SubItems)
```