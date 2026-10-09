new DataStore(){ a, {b, c}} as long as there is one Add() method whose signature is compatible with a and a second Add() method whose signature is compatible with b, c.

# # What Makes a Class a Collection: IEnumerable<T>

By definition, a collection within .NET is a class that, at a minimum, implements IEnumerable<T> (or the nongeneric type IEnumerable). This interface is critical because implementing the methods of IEnumerable<T> is the minimum needed to support iterating over the collection.

Chapter 4 showed how to use a foreach statement to iterate over an array of elements. This syntax is simple and avoids the complication of having to know how many elements there are. The runtime does not directly support the foreach statement, however. Instead, the C# compiler transforms the code as described in this section.

# ## foreach with Arrays

Listing 15.3 demonstrates a simple foreach loop iterating over an array of integers and then printing out each integer to the console.

```
**LISTING 15.3:** foreach with Arrays

`int[] array = new int[]{1, 2, 3, 4, 5, 6};

foreach (int item in array)
{
    Console.WriteLine(item);
}`
```

From this code, the C# compiler creates a CIL equivalent of the for loop, as shown in Listing 15.4.

```
**LISTING 15.4:** Compiled Implementation of foreach with Arrays

`int[] tempArray;
int[] array = new int[]{1, 2, 3, 4, 5, 6};

tempArray = array;
for (int counter = 0; (counter < tempArray.Length); counter++)
{
    int item = tempArray[counter];

    Console.WriteLine(item);
}`
```