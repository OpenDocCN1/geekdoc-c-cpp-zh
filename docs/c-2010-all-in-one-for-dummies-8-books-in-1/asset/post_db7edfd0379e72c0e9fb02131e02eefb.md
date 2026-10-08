
## 120 New Feature: Using var for Arrays

Figure 6-5: The final pass terminates the sort because nothing changes.

| Earth | Description |
| :--- | :--- |
| Earth | At the finish, it's Earth crossing the line in first place for the win... |
| Jupiter | ...and Jupiter needs out Mars to place. |
| Mars | Meanwhile, Mars struggles to show. |
| Mercury | |
| Venus | |

Eventually, longer planet names "bubble" their way to the top of the list; hence the name bubble sort.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_145_0.png)

Give single-item variables names, as in planet or student. The name of the variable should somehow include the name of the class, as in badStudent or goodStudent or sexyCodeDict. Arrays (or other collections) plural names, as in students or phoneNumbers or phoneInMyPalmPilot. As always, this reflects the opinion of the authors and not of this book's publisher nor any of its shareholders— C# doesn't care how you name your variables.

## New Feature: Using var for Arrays

Traditionally, you used one of the following forms (which are as old as C# six years old at the time this book was written) to initialize an array:

```csharp
int[] numbers = new int[3];              // Size no initializer, or \
int[] numbers = new int[] { 1, 2, 3 }; // Initializer but no size, or \
int[] numbers = new int[] { 1, 2, 3 };   // Size and initializer, or ... \
int numbers = { 1, 2, 3 };               // No 'new' keyword -- extreme short form.
```

Chapter 2 of this minibook introduces the new var keyword, which tells the C# compiler, "You figure out the variable type by the initializer expression I'm providing."

Happily, `var arrays = arrays`, works too:

```csharp
var myArray = new int[] { 2, 3, 5, 7, 11, 13 }; // Initializer required!
```

The syntax has only two changes:

- var is used instead of the explicit type information for the numbers on the left side of the assignment.
- int keyword is omitted before the brackets on the right side of the assignment. It's the part that the compiler can infer.

## Loosening Up with C# Collections

In the var version, the initializer is required. The compiler uses it to infer the type of the array elements without the int keyword.

Here are a few more examples:

```csharp
var names = new [] { "John", "Paul", "George", "Ringo" };
var averages = new [] { 3.0, 3.34, 4.0, 2.0, 1.8 };
var prez = new [] { new President("FDR"), new President("JFK") };
```

You can't use the extreme form for initializing an array when you use var. The following line doesn't compile:

```csharp
var names = { "John", "Paul", "George", "Ringo" }; // Needs 'new []'
```

The var is less concise, but when used in other situations not involving arrays, it truly shines and in some cases is not mandatory. You can see examples in Chapter 7.

The UsingVarArraysAndCollections sample program on this book's Web demonstrates var array initializes. Note that you can't use var as a variable name now, or you in the past. It's a crummy name anyway.

## Loosening Up with C# Collections

Often an array is the simplest, most straightforward way to deal with a list of Students or a list of doubles. You also encounter many places in the .NET Framework class library that require the use of arrays.

But arrays have a couple of fairly serious limitations that get in your way. At such times, you'll appreciate the extensive C# repertoire of more flexible collection classes.

Although arrays have the advantage of simplicity and can have multiple dimensions, they suffer from two important limitations:

- A program must declare the size of an array when it's created. Unlike Visual Basic, C# doesn't let you change the size of an array after it's defined. For example, you might not know up front how big the array needs to be.
- Inserting or removing an element in the middle of an array is wildly inefficient. You have to move around all the elements to make room. In a big array, that can be a huge, time-consuming job.

Most collections, the other hand, make it much easier to add, insert, or remove elements, and you can resize them as needed. In fact, most collections take care of resizing automatically.

If you need a multidimensional structure, use an array. No collection allows multiple dimensions (although you can create some elaborate structures as collections of collections).

Arrays and collections have some characteristics in common:

- Each contain elements of only one type. You must specify that type in your code at compile time, and after you declare the type, it can change.
- As arrays, you can access most collections with array-like syntax using square brackets to specify an index: `list[3]`.
- Both collections and arrays have methods and properties. To find the number of elements in the following `smallNumbers` array, you call its `Length` property:

```csharp
var smallNumbers = new int[] { 2, 3, 5, 7, 11, 13 };
int numElements = smallNumbers.Length; // Result is 6.
```

With a collection, you call its `Count` property:

```csharp
List<int> smallPrimes = new List<int> { 2, 3, 5, 7, 11, 13 };
int numElements = smallPrimes.Count; // Collections have Count property.
```

Check out `Array` to see what other methods and properties it has (properties and methods).

In this section, I'll get you up and running with collection syntax and introduce the most important and used collection classes. Table 6-1 lists the main collection classes in C#. I find it useful to think of collections as having varying "shapes"—the list or dictionary, for example.

| Class | Description |
| :--- | :--- |
| List<T> | This dynamic array contains objects of T. |
| LinkedList<T> | This is a linked list of objects of T. |
| Queue<T> | Start at the back of the line and end up at the front. |
| Stack<T> | Always add or delete items at the "top" of the list, like a stack of cafeteria trays. |
| Dictionary<TKey, TValue> | This structure works like a dictionary. Look up a key (a word, for example) and retrieve its corresponding value (for example). |
| HashSet<T> | This structure resembles a mathematical set, with no duplicate items. It works like a list but provides mathematical operations, such as union and intersection. |

## Figure out <T>

In the mysterious-looking <T> notation you see in Table 6-1, <T> is a placeholder for a particular data type. To bring this symbolic object to life, instantiate it by inserting a real type, like this:

```csharp
List<int> intList = new List<int>(); // Instantating for int
```

Instantiate is geekspeak for “Create an object (instance) of this type.”

For example, you might create different List<T> instillations for types int, string, and Student. By the way, T is not a sacred name. You can use anything like it—for instance, <dummy> or <a>. It's common to use T, U, V, and so on.

Notice how I express the Dictionary<TKey, TValue> collection in Table 6-1. Here, two types are needed: one for the dictionary’s keys and one for the values associated with the keys. I cover dictionaries later in the section “Using Dictionaries.”

If this notation seems a bit formidable, don't worry. You get used to it.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_148_0.png)

## Going generic

These modern collections are known as generic collections in the sense that you can fill in a blank template, of sorts, with a <type> (or types) in order to create a custom collection. If the generic List<T> seems puzzling, check out Chapter 8 in this minibook. That chapter discusses the generic C# facilities in more detail. In particular, the chapter shows how to use your generic collections, classes, methods, and other types.

## Using Lists

Suppose you need to store a list of MP3 objects, each of which represents one item in your MP3 music collection. As an array, it might look like this:

```csharp
myMP3 = new MP3[50]; // Start with an empty array.
myMP3[0] = new MP3("Norah Jones"); // Create an MP3 and add it to the array.
// and so on.
```

With a list, it looks like this:

```csharp
List<MP3> myMP3s = new List<MP3>(); // An empty list
myMP3s.Add(new MP3("Avril Lavigne")); // Call the list's Add method to add.
// and so on.
```

So, you say? These examples look similar, and the list doesn't appear to provide any advantage over the array. But what happens when you add the 50th MP3 to the array and then want to add a 51st? You're out of room. Your only course is to declare a new, larger array and then copy all MP3s from the old array into the new one. Also, if you remove an MP3 from the array, your array is left with a gaping slot to take the place of the MP3 you ditched. The value null, maybe

The list collection happily handles, in the face of these same obstacles. Want to add MP3 51st? No problem. Want to join your old Pat Boone MP3s? (Are there any?) No problem. The list takes care of healing itself after you delete old Pat.

If your list (or array, for that matter) can contain null items, be sure to check for null when you're looping with for or foreach. You don't want to call the Play() method on a null MP3 item. It returns in error.
