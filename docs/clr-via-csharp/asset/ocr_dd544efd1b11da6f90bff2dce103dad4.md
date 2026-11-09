The new generic interfaces are not a replacement for the old non-generic interfaces; in many scenarios, you will have to use both. The reason is backward compatibility. For example, if the `List<T>` class implemented only the `IList<T>` interface, no code could consider a `List<DateTime>` object an `IList`.

I should also point out that the **System.Array** class, the base class of all array types, offers many static generic methods, such as **AsReadOnly, BinarySearch, ConvertAll, Exists, Find, FindAll, FindIndex, FindLast, FindLastIndex, ForEach, IndexOf, LastIndexOf, Resize, Sort,** and **TrueForAll**. Here are examples showing what some of these methods look like:

```
```csharp
public abstract class Array : ICloneable, IList, ICollection, IEnumerable,
    IStructuralComparable, IStructuralEquatable {

    public static void Sort<T>(T[] array);
    public static void Sort<T>(T[] array, IComparer<T> comparer);

    public static Int32 BinarySearch<T>(T[] array, T value);
    public static Int32 BinarySearch<T>(T[] array, T value,
        IComparer<T> comparer);
}
...
```
```

Here is code that demonstrates how to use some of these methods:

```
```csharp
public static void Main() {
    // Create & initialize a byte array
    Byte[] byteArray = new Byte[] { 5, 1, 4, 2, 3 };

    // Call Byte[] sort algorithm
    Array.Sort<Byte>(byteArray);

    // Call Byte[] binary search algorithm
    Int32 i = Array.BinarySearch<Byte>(byteArray, 1);
    Console.WriteLine(i);   // Displays "0"
}
```
```

# # Wintellect’s Power Collections Library

At Microsoft’s request, Wintellect has produced the Power Collections library to bring some of the C++ Standard Template Library’s collection classes to the CLR programmer. This library is a set of collection classes that anyone can download and use free of charge. See *http://Wintellect.com* for details. These collection classes are generic themselves and make extensive use of generics. Table 12-1 shows a list of some of the collection classes you’ll find in the Power Collections library.