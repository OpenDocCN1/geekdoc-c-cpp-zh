
These statements print out the array in sorted order:

```
1
2
3
4
5
```

### Accessing Array Elements

To access an element in an array, you specify its index, as shown in the following statements:

```csharp
int[] num = new int[5] { 1, 2, 3, 4, 5 };
Console.WriteLine(num[0]); //---1---
Console.WriteLine(num[1]); //---2---
Console.WriteLine(num[2]); //---3---
Console.WriteLine(num[3]); //---4---
Console.WriteLine(num[4]); //---5---
```

The index of an array starts from 0 to *n*-1. For example, num has size of 5 so the index runs from 0 to 4.

You usually use a loop construct to run through the elements in an array. For example, you can use the `for` statement to iterate through the elements of an array:

```csharp
for (int i = 0; i < num.Length; i++)
    Console.WriteLine(num[i]);
```

You can also use the `foreach` statement, which is a clean way to iterate through the elements of an array quickly:

```csharp
foreach (int n in num)
    Console.WriteLine(n);
```

### Multidimensional Arrays

So far the arrays you have seen are all one-dimensional ones. Arrays may also be multidimensional. To declare a multidimensional array, you can use the comma (,) separator. The following declares xy to be a 2-dimensional array:

```csharp
int[,] xy;
```

To initialize the two-dimensional array, you use the `new` keyword together with the size of the array:

```csharp
xy = new int[3,2];
```

With this statement, xy can now contain six elements (three rows and two columns). To initialize xy with some values, you can use the following statement:

```csharp
xy = new int[3, 2] { { 1, 2 }, { 3, 4 }, { 5, 6 } };
```

The following statement declares a three-dimensional array:

```csharp
int[,,] xyz;
```

To initialize it, you again use the new keyword together with the size of the array:

```csharp
xyz = new int[2, 2, 2];
```

To initialize the array with some values, you can use the following:

```csharp
int[,,] xyz;
xyz = new int[,,] {
  { { 1, 2 }, { 3, 4 } },
  { { 5, 6 }, { 7, 8 } }
};
```

To access all the elements in the three-dimensional array, you can use the following code snippet:

```csharp
for (int x = xyz.GetLowerBound(0); x <= xyz.GetUpperBound(0); x++)
  for (int y = xyz.GetLowerBound(1); y <= xyz.GetUpperBound(1); y++)
    for (int z = xyz.GetLowerBound(2); z <= xyz.GetUpperBound(2); z++)
      Console.WriteLine(xyz[x, y, z]);
```

The Array abstract base class contains the GetLowerBound() and GetUpperBound() methods to let you know the size of an array. Both methods take in a single parameter, which indicates the dimension of the array about which you are inquiring. For example, GetUpperBound(0) returns the size of the first dimension, GetUpperBound(1) returns the size of the second dimension, and so on.

You can also use the foreach statement to access all the elements in a multidimensional array:

```csharp
foreach (int n in xyz)
  Console.WriteLine(n);
```

These statements print out the following:

```
1
2
3
4
5
6
7
8
```

### Arrays of Arrays: Jagged Arrays

An array's elements can also contain arrays. An array of arrays is known as a jagged array. Consider the following statements:

```csharp
Point[][] lines = new Point[5][];
lines[0] = new Point[4];
lines[1] = new Point[15];
lines[2] = new Point[7];
lines[3] = ...
lines[4] = ...
```

Here, lines is a jagged array. It has five elements and each element is a Point array. The first element is an array containing four elements, the second contains 15 elements, and so on.

> *The Point class represents an ordered pair of integer x- and y-coordinates that defines a point in a two-dimensional plane.*

You can use the array initializer to initialize the individual array within the lines array, like this:

```csharp
Point[][] lines = new Point[3][];
lines[0] = new Point[] {
    new Point(2, 3), new Point(4, 5)
}; //---2 points in lines[0]---

lines[1] = new Point[] {
    new Point(2, 3), new Point(4, 5) , new Point(6, 9)
}; //---3 points in lines[1]---

lines[2] = new Point[] {
    new Point(2, 3)
}; //---1 point in lines[2]---
```

To access the individual Point objects in the lines array, you first specify which Point array you want to access, followed by the index for the elements in the Point array, like this:

```csharp
//---get the first point in lines[0]---
Point ptA = lines[0][0]; //---(2,3)---

//---get the third point in lines[1]---
Point ptB = lines[1][2]; //---(6,9)---
```

A jagged array can also contain multidimensional arrays. For example, the following declaration declares nums to be a jagged array with each element pointing to a two-dimensional array:

```csharp
int[][,] nums = new int[][,]
{
    new int[,] { {1, 2}, {3, 4} },
    new int[,] { {5, 6}, {7, 8} }
};
```

To access an individual element within the jagged array, you can use the following statements:

```csharp
Console.WriteLine(nums[0][0, 0]); //---1---
Console.WriteLine(nums[0][0, 1]); //---2---
Console.WriteLine(nums[0][1, 0]); //---3---
Console.WriteLine(nums[0][1, 1]); //---4---
Console.WriteLine(nums[1][0, 0]); //---5---
Console.WriteLine(nums[1][0, 1]); //---6---
Console.WriteLine(nums[1][1, 0]); //---7---
Console.WriteLine(nums[1][1, 1]); //---8---
```

Used on a jagged array, the Length property of the Array abstract base class returns the number of arrays contained in the jagged array:

```csharp
Console.WriteLine(nums.Length); //---2---
```

### Parameter Arrays

In C#, you can pass variable numbers of parameters into a function/method using a feature known as parameter arrays. Consider the following statements:

```csharp
string firstName = "Wei-Meng";
string lastName = "Lee";
Console.WriteLine("Hello, {0}", firstName);
Console.WriteLine("Hello, {0} {1}", firstName, lastName);
```

Observe that the last two statements contain different numbers of parameters. In fact, the WriteLine() method is overloaded, and one of the overloaded methods has a parameter of type params (see Figure 13-3). The params keyword lets you specify a method parameter that takes an argument where the number of arguments is variable.

![](img/a977a875c7c627b45d939729705a252e_426_0.png)

A result of declaring the parameter type to be of params is that callers to the method do not need to explicitly create an array to pass into the method. Instead, they can simply pass in a variable number of parameters.

To use the params type in your own function, you define a parameter with the params keyword:

```csharp
private void PrintMessage(string prefix, params string[] msg)
{
}
```

To extract the parameter array passed in by the caller, treat the params parameter like a normal array, like this:

```csharp
private void PrintMessage(string prefix, params string[] msg)
{
    foreach (string s in msg)
        Console.WriteLine("{0}>{1}", prefix, s);
}
```

When calling the PrintMessage() function, you can pass in a variable number of parameters:

```csharp
PrintMessage("C# Part 1", "Arrays", "Index", "Collections");
PrintMessage("C# Part 2", "Objects", "Classes");
```

These statements generate the following output:

```
C# Part 1>Arrays
C# Part 1>Index
C# Part 1>Collections
C# Part 2>Objects
C# Part 2>Classes
```

> A params parameter must always be the last parameter defined in a method declaration.

### Copying Arrays

To copy from one array to another, use the Copy() method from the Array abstract base class:

```csharp
int[] num = new int[5] { 1, 2, 3, 4, 5 };
int[] num1 = new int[5];
num.CopyTo(num1, 0);
```

These statements copy all the elements from the num array into the num1 array. The second parameter in the CopyTo() method specifies the index in the array at which the copying begins.

### Collections Interfaces

The System.Collections namespace contains several interfaces that define basic collection functionalities: The interfaces described in the following list are the generic versions of the respective interfaces. Beginning with C# 2.0, you should always try to use the generic versions of the interfaces for type safety. Chapter 9 discusses the use of generics in the C# language.

| Interface | Description |
|---|---|
| IEnumerable<T> and IEnumerator<T> | Enable you to loop through the elements in a collection. |
| ICollection<T> | Contains items in a collection and provides the functionality to copy elements to an array. Inherits from IEnumerable<T>. |
| IComparer<T> and IComparable<T> | Enable you to compare objects in a collection. |
| IList<T> | Inherits from ICollection<T> and provides functionality to allow members to be accessed by index. |
| IDictionary<K,V> | Similar to IList<T>, but members are accessed by key value rather than index. |

The ICollection<T> interface is the base interface for classes in the System.Collections namespace.

### Dynamic Arrays Using the ArrayList Class

Arrays in C# have a fixed size once they are initialized. For example, the following defines a fixed-size array of five integer elements:

```csharp
int[] num = new int[5];
```

If you need to dynamically increase the size of an array during runtime, use the ArrayList class instead. You use it like an array, but its size can be increased dynamically as required.

The ArrayList class is located within the System.Collections namespace, so you need to import that System.Collections namespace before you use it. The ArrayList class implements the IList interface.

To use the ArrayList class, you first create an instance of it:

```csharp
ArrayList arrayList = new ArrayList();
```

Use the Add() method to add elements to an ArrayList object:

```csharp
arrayList.Add("Hello");
arrayList.Add(25);
arrayList.Add(new Point(3,4));
arrayList.Add(3.14F);
```

Notice that you can add elements of different types to an ArrayList object.
