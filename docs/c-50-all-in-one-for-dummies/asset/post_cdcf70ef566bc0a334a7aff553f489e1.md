
```c
Console.WriteLine("\nPress Enter to terminate...");
Console.Read();
}
}
```

The program begins with an array containing the names of the first five planets closest to the sun. (To keep the figures small, I didn’t include the outer planets, so I didn’t have to decide about poor Pluto, which is, what now? — a dwarf planet or something?)

The program then invokes the array’s own Sort() method. After sorting with the built-in Sort() method on the Array class, the program sorts the lengths of the planets’ names using a custom sort just to amaze you.

![](img/6df7bb88e9302e98442acc219cfbd7fc_142_0.png)

The built-in Sort() method for arrays (and other collections) is, without a doubt, more efficient than the custom bubble sort. Don’t roll your own unless you have good reason to.

The algorithm for the second sort works by continuously looping through the list of strings until the list is sorted. On each pass through the sortedNames array, the program compares each string to its neighbor. If the two are found to be out of order, the method swaps them and then flags the list as not sorted. Figures 6-2 through 6-5 show the planets list after each pass. In Figure 6-5, note that the next-to-last pass results in a sorted list and that the final pass terminates the sort because nothing changes.

Figure 6-2:
Before starting the bubble sort.

| Mercury ← And they’re off and running! |
| :--- |
| Venus |
| Earth |
| Mars |
| Jupiter |

Figure 6-3:
After Pass 1 of the bubble sort.

| Earth ← Earth edges its way into the lead... |
| :--- |
| Mercury |
| Venus |
| Mars |
| Jupiter |

Figure 6-4:
After Pass 2 of the bubble sort.

| Earth |
| Mars ← Mars jumps past Mercury and Venus for second place |
| Mercury |
| Venus |
| Jupiter |

Figure 6-5:
The final pass terminates the sort because nothing changes.

| Earth ← At the finish, it’s Earth crossing the line in first place for the win... |
| Jupiter ← ...and Jupiter noses out Mars to place. |
| Mars ← Meanwhile, Mars struggles to show. |
| Mercury |
| Venus |

Eventually, longer planet names “bubble” their way to the top of the list; hence the name bubble sort.

![](img/6df7bb88e9302e98442acc219cfbd7fc_143_0.png)

Give single-item variables singular names, as in planet or student. The name of the variable should somehow include the name of the class, as in badStudent or goodStudent or sexyCoedStudent. Give arrays (or other collections) plural names, as in students or phoneNumbers or phoneNumbersInMyPalmPilot. As always, this tip reflects the opinion of the author and not of this book’s publisher nor any of its shareholders — C# doesn’t care how you name your variables.

# Using var for Arrays

Traditionally, you used one of the following forms (which are as old as C# — almost ten years old at the time this book was written) to initialize an array:

```csharp
int[] numbers = new int[3];                 // Size but no initializer, or ...
int[] numbers = new int[] { 1, 2, 3 };      // Initializer but no size, or ...
int[] numbers = new int[3] { 1, 2, 3 };     // Size and initializer, or ...
int[] numbers = { 1, 2, 3 };                // No 'new' keyword -- extreme short form.
```

Chapter 2 of this minibook introduces the var keyword, which tells the C# compiler, “You figure out the variable type from the initializer expression I’m providing.”

Happily, var works with arrays, too:

```csharp
// myArray is an int[] with 6 elements.
var myArray = new [] { 2, 3, 5, 7, 11, 13 }; // Initializer required!
```

The new syntax has only two changes:

- var is used instead of the explicit type information for the numbers array on the left side of the assignment.
- The int keyword is omitted before the brackets on the right side of the assignment. It's the part that the compiler can infer.

In the var version, the initializer is required. The compiler uses it to infer the type of the array elements without the int keyword.

Here are a few more examples:

```csharp
var names = new [] { "John", "Paul", "George", "Ringo" }; // Strings
var averages = new [] { 3.0, 3.34, 4.0, 2.0, 1.8 }; // Doubles
var prez = new []{new President("FDR"), new President("JFK")}; // Presidents
```

You can't use the extreme short form for initializing an array when you use var. The following line doesn't compile:

```csharp
var names = { "John", "Paul", "George", "Ringo" }; // Needs 'new []'
```

The var way is less concise, but when used in some other situations not involving arrays, it truly shines and in some cases is mandatory. (You can see examples in Book I, Chapter 7.)

The UsingVarWithArraysAndCollections sample program on this book demonstrates var with array initializers. Note that you can't use var as a variable name anymore.

# Loosening Up with C# Collections

Often an array is the simplest, most straightforward way to deal with a list of students or doubles. You also encounter many places in the .NET Framework class that require the use of arrays.

But arrays have a couple of serious limitations that sometimes get in your way. At such times, you'll appreciate the extensive repertoire of flexible collection classes.

Although arrays have the advantage of simplicity and can have multiple dimensions, they suffer from important limitations:

![](img/6df7bb88e9302e98442acc219cfbd7fc_144_0.png)
![](img/6df7bb88e9302e98442acc219cfbd7fc_144_1.png)
![](img/6df7bb88e9302e98442acc219cfbd7fc_144_2.png)

- **A program must declare the size of an array when it’s created.** Unlike Visual Basic, C# doesn’t let you change the size of an array after it's defined. For example, you might not know how big the array needs to be.
- **Inserting or removing an element in the middle of an array is inefficient.** You have to move around all the elements to make room. Most collections, on the other hand, make it easier to add, insert, or remove elements, and you can resize them as needed. In fact, most collections take care of resizing automatically.

![](img/6df7bb88e9302e98442acc219cfbd7fc_145_0.png)

If you need a multidimensional structure, use an array. No collection allows multiple dimensions (although you can create elaborate structures, such as collections of collections). Arrays and collections have some common characteristics:

- Each contains elements of only one type. You must specify that type at compile time, and after you declare the type, it can't change.
- As with arrays, you can access most collections with array-like syntax using square brackets: myList[3] = "Joe".
- Both collections and arrays have methods and properties. Thus, to find the number of elements in the following smallPrimeNumbers array, you call its Length property:

```csharp
var smallPrimeNumbers = new [] { 2, 3, 5, 7, 11, 13 };
int numElements = smallPrimeNumbers.Length; // Result is 6.
```

With a collection, you call its Count property:

```csharp
List<int> smallPrimes = new List<int> { 2, 3, 5, 7, 11, 13 };
int numElements = smallPrimes.Count; // Collections have a Count property.
```

Check out the Array class in Help to see what other methods and properties it has (7 public properties and 36 public methods).

# Understanding Collection Syntax

In this section, I get you up and running with collection syntax and introduce the most important and frequently used collection classes. Table 6-1 lists the main collection classes in C#. I find it useful to think of collections as having various “shapes” — the list shape or dictionary shape, for example.

| Table 6-1 The Most Common Collection "Shapes" | |
| :--- | :--- |
| Class | Description |
| List<T> | This dynamic array contains objects of type T. |
| LinkedList<T> | This is a linked list of objects of type T. |
| Queue<T> | Start at the back end of the line and end up at the front. |
| Stack<T> | Always add or delete items at the "top" of the list, like a stack of cafeteria trays. |
| Dictionary<TKey, TValue> | This structure works like a dictionary. Look up a key (a word, for example) and retrieve its corresponding value (for example, definition). |
| HashSet<T> | This structure resembles a mathematical set, with no duplicate items. It works much like a list but provides mathematical set operations, such as union and intersection. |

# Figuring out <T>

In the mysterious-looking <T> notation you see in Table 6-1, <T> is a placeholder for a particular data type. To bring this symbolic object to life, instantiate it by inserting a real type, like this:

```csharp
List<int> intList = new List<int>(); // Instantiating for int
```

Instantiate is geekspeak for "Create an object (instance) of this type."

For example, you might create different List<T> instantiations for types int, string, and Student, for example. By the way, T isn't a sacred name. You can use anything you like — for instance, <dummy> or <aType>. It's common to use T, U, V, and so on.

Notice how I express the Dictionary<TKey, TValue> collection in Table 6-1. Here, two types are needed: one for the dictionary's keys and one for the values associated with the keys. I cover dictionaries later, in the section "Using Dictionaries."

If this notation seems a bit forbidding, don't worry. You get used to it.

# Going generic

These modern collections are known as generic collections, in the sense that you can fill in a blank template, of sorts, with a type (or types) in order to create a custom collection. If the generic List<T> seems puzzling, check out Chapter 8 in this minibook. That chapter discusses the generic C# facilities in more detail.
