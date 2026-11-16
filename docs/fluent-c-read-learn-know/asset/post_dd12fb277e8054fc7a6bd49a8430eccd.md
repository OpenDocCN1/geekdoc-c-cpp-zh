
![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_373_0.png)

### HOW'D YOU DO?

How would you write a foreach statement that did something for every element in an Array of Int32s called ValidDates?

```
For Each (Int32 i in ValidDates) {}
```

It doesn't matter what you called the control variable here, as long as it's a valid identifier and not a keyword.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_373_1.png)

### PUT ON YOUR THINKING HAT

Using the Object Browser and MSDN, can you write the following statements using the members of the Array class?

- Set an Int32 called NumElements to the number of elements in the array MyDays:
- Sort the Array called Names using the default comparison method for Strings:
- Find the last instance of “Hello” in an array of Strings called words. (You’ll need to define the predicate as well.):

### HOW'D YOU DO?

Set an Int32 called NumElements to the number of elements in the array MyDays:

```
NumElements = MyDays.Length;
```

Sort the Array called Names using the default comparison method for Strings:

```
Array.Sort(Names);
```

Find the last instance of “Hello” in an Array of Strings called words. (You’ll need to define the predicate as well):

```
Boolean IsHello(String test)
{
    if (test == "Hello")
        return true;
    else
        return false;
}
```

```
Array.FindLast(words, IsHello);
```

### TAKE A BREAK

Now that we’ve gotten a taste of how to handle sets of objects using the Array class, why don’t you take a break before we move on to some of the specialized set types provided by the .NET Framework?

## SPECIALIZED SETS

The Array class is supported by the C# compiler, its elements are simple to access, and it provides some basic methods for manipulating its contents. But the Array is a value type, and as such is immutable, which can make operations such as sorting elements or re-sizing the array an expensive operation. The solution, of course, is to use a reference type when you need to perform operations like these, and the .NET Framework provides several.

Most of the .NET Framework set types come in two versions, one that manipulates elements as Object types, and one that allows elements to be strongly typed through the use of generic parameters that are specified when the class is instantiated. We'll look at the types that use Object elements in this section, and examine the strongly typed GENERIC versions in the next.

### THE ARRAYLIST CLASS

You can think of the ArrayList class as an Array that contains reference types, but it does have slightly different capabilities. The ArrayList is always one-dimensional (as, in practice, most Arrays are), and its elements are always instances of the Object type, so you must cast them, and value type elements will be boxed.

On the other hand, the size of an ArrayList isn't fixed, and you can insert elements at any position without re-creating the set, and because the elements are Objects, you can search the set without using a predicate.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_375_0.png)

### THE SET INTERFACES

Here's a partial class diagram of the ArrayList. As you can see, the ArrayList implements several interfaces but descends directly from System.Object. These interfaces, ICollection, IList and IEnumerable, define the basic functionality of set types in the .NET Framework, are implemented by most of the set types, including the basic Array we looked at in the last section.

Internally, the ArrayList stores its data as a basic Array, but the behavior it exposes makes it dynamic: You can insert and delete items at any position, and the ArrayList will take care of resizing and re-ordering the data for you. But be aware that this capability doesn't come for free. The ArrayList does the memory allocations for you, but they're still being done, and they still take time.

The IEnumerable interface allows the foreach statement to be used with an ArrayList.

The ICollection interface extends IEnumerable, adding, among other things, the Count property and the CopyTo() method that creates a standard Array from the ArrayList.

IList extends ICollection, and allows elements to be accessed by their index.

ICloneable allows copies of the object to be created.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_376_0.png)

When you Add() a new item to an ArrayList, it will expand the Capacity for you as necessary.

The Capacity of an ArrayList is the number of items it can currently hold. The Count is the number of items it currently holds.

### PUT ON YOUR THINKING HAT

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_377_0.png)

Using the class diagram, the Object Browser and MSDN, can you write statements to perform the following functions?

The default constructor creates an ArrayList with a capacity of 4. If you know in advance that you'll have ten items, what constructor will be more efficient? Write the statement to declare and initialize an ArrayList called MyAL:

Set the third item in MyAL to “Hello”:

Insert “World” as a new item at the end of the MyAL:

Remove the fourth item in MyAL:

Determine whether MyAL contains “Hello”:

Insert “Hello, World” at the seventh position in MyAL:

### HOW'D YOU DO?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_378_0.png)

The default constructor creates an ArrayList with a capacity of 4. If you know in advance that you'll have 10 items, what constructor will be more efficient? Write the statement to declare and initialize an ArrayList called MyAL:

```
ArrayList MyAL = new ArrayList(10);
```

### Set the third item in MyAL to "Hello":

```
MyAL[2] = "Hello";
```

Give yourself a gold star if you remembered that the first item is zero, not one

### Insert "World" as a new item, at the end of the MyAL:

```
MyAL.Add("World");
```

You could also have used something like `MyAL[MyAL.Count - 1] = "World"` but that would be far more complicated...

### Remove the 4th item in MyAL:

```
MyAL.Remove(3);
```

If you used the Remove() method, go back and check the difference between Remove() and RemoveAt(). But don't feel bad; it's a common mistake.

### Determine whether MyAL contains "Hello":

```
MyAL.Contains("Hello");
```

A lot easier than the Array version, isn't it?

### Insert "Hello, World" at the 7th position in MyAL:

```
MyAL.Insert(6, "Hello, World");
```

## LIFO, FIFO, LINKS & KEYS

Both the Array and the ArrayList contain elements that can be accessed in any order. You can sort them, of course, or add the elements in a particular order, but by default the elements are stored randomly. The .NET Framework also supports classes that allow their elements to be accessed in particular ways.

Push() puts new item on the top of the stack.

Pop() takes the top item off the top of the stack.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_379_0.png)

You can only access the top element on the stack.

You've already met the stack. It stores its elements in LIFO order, which is pronounced "Life-oh", and stands for Last In, First Out.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_379_1.png)

The Hashtable and Dictionary store items in key/value pairs. The keys of a Dictionary must be unique. Hash codes don't have to be, but it's best if they are.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_379_2.png)

In a linked list, each item knows about the item in front of and behind it. We'll talk about the LinkedList<T> class in the next section.

Enqueue() adds an item to the end of the line.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_379_3.png)

Dequeue() takes an element from the head of the line.

The Queue stores its elements in FIFO order, which is pronounced "Fife-oh", and stands for First In, First Out.

### PUT ON YOUR THINKING HAT

Looking back at the descriptions of the different kinds of set types, can you match each of these real-world examples to its programming equivalent?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_380_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_380_1.png)

A line of people expect to be served in the order they arrived. It's like a:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_380_2.png)

A Rolodex has one card for every phone number. It's like a:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_380_3.png)

A dictionary has a single entry for a word, but a word can have multiple meanings. It's like a:
