# Chapter 15: Collection Interfaces with Standard Query Operators

LISTING 15.4: Compiled Implementation of foreach with Arrays

```
int[] tempArray;
int[] array = new int[] { 1, 2, 3, 4, 5, 6 };

tempArray = array;
for(int counter = 0; counter < tempArray.Length; counter++)
{
    int item = tempArray[counter];
    Console.WriteLine(item);
}
```

In this example, note that foreach relies on support for the Length property and the index operator ([]). With the Length property, the C# compiler can use the for statement to iterate through each element in the array.

# foreach with IEnumerable<T>

Although the code shown in Listing 15.4 works well on arrays where the length is fixed and the indexer is always supported, not all types of collections have a known number of elements. Furthermore, many collection classes, including the Stack<T>, Queue<T>, and Dictionary<TKey, TValue> classes, do not support retrieving elements by index. Therefore, a more general approach of iterating over collections of elements provides this capability. Assuming you can determine the first and next elements, knowing the count and supporting retrieval of elements by index is unnecessary.

The System.Collections.Generic.IEnumerable<T> and nongraphic System.Collections.Enumerator interfaces are designed to enable the iterator pattern for iterating over collections, rather than the length–index pattern shown in Listing 15.4. A class diagram of their relationships appears in Figure 15.1.

IEnumerator, which IEnumerator<T> derives from, includes three members. The first is bool MoveNext(). Using this method, you can move from one element within the collection to the next, while at the same time detecting when you have enumerated through every item. The second member, a read-only property called Current, returns the element currently in process. Current is overloaded in IEnumerator<T>, providing a type-specific implementation of it. With these