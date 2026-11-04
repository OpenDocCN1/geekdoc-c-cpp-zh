To access an element contained within an ArrayList object, specify the element's index like this:

```
```csharp
Console.WriteLine(arrayList[0]); //---Hello---
Console.WriteLine(arrayList[1]); //---25---
Console.WriteLine(arrayList[2]); //---{X=3, Y=4}
Console.WriteLine(arrayList[3]); //---3.14---
```
```

The ArrayList object can contain elements of different types, so when retrieving items from an ArrayList object make sure that the elements are assigned to variables of the correct type. Elements retrieved from an ArrayList object belong to Object type.

You can insert elements to an ArrayList object using the Insert() method:

```
```csharp
arrayList.Insert(1, " World!");
```
```

After the insertion, the ArrayList object now has five elements:

```
```csharp
Console.WriteLine(arrayList[0]); //---Hello---
Console.WriteLine(arrayList[1]); //---World!---
Console.WriteLine(arrayList[2]); //---25---
Console.WriteLine(arrayList[3]); //---{X=3, Y=4}---
Console.WriteLine(arrayList[4]); //---3.14---
```
```

To remove elements from an ArrayList object, use the Remove() or RemoveAt() methods:

```
```csharp
arrayList.Remove("Hello");
arrayList.Remove("Hi"); //---cannot find item---
arrayList.Remove(new Point(3, 4));
arrayList.RemoveAt(1);
```
```

After these statements run, the ArrayList object has only two elements:

```
```csharp
Console.WriteLine(arrayList[0]); //---World!---
Console.WriteLine(arrayList[1]); //---3.14---
```
```

If you try to remove an element that is nonexistent, no exception is raised (which is not very useful). It would be good to use the Contains() method to check whether the element exists before attempting to remove it:

```
```csharp
if (arrayList.Contains("Hi"))
    arrayList.Remove("Hi");
else
    Console.WriteLine("Element not found.");
```
```

You can also assign the elements in an ArrayList object to an array using the ToArray() method:

```
```csharp
object[] objArray;
objArray = arrayList.ToArray();

foreach (object o in objArray)
    Console.WriteLine(o.ToString());
```
```