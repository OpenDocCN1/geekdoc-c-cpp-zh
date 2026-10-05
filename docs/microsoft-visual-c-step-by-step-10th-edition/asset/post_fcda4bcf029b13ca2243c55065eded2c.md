
item in a collection use the Find method. For example:

Click here to view code image

```
Dictionary<string, int> ages = new Dictionary<string,
int>();
ages.Add("John", 47);
int johnAge = ages["John"];
...
List<Person> personnel = new List<Person>();
Person match = personnel.Find(p => p.ID == 3);
```

Iterate through the elements of a collection Use a for statement or a foreach statement. For example:

Click here to view code image

```
LinkedList<int> numbers = new LinkedList<int>();
...
for (LinkedListNode<int> node = numbers.First; node is
not null; node = node.Next)
{
  int number = node.Value;
  Console.WriteLine(number);
}
...
foreach (int number in numbers)
{
  Console.WriteLine(number);
}
```

# Chapter 19

# Enumerating collections

After completing this chapter, you will be able to:

- Manually define an enumerator that you can use to iterate over the elements in a collection.
- Implement an enumerator automatically by creating an iterator.
- Provide additional iterators that step through the elements of a collection in different sequences.

Chapter 10, “Using arrays,” and Chapter 18, “Using collections,” showed how to use arrays and collection classes to hold sequences or sets of data. Chapter 10 also detailed the foreach statement, which you can use to step through, or iterate over, the elements in a collection. In those cases, you used the foreach statement as a quick and convenient way of accessing the contents of an array or collection, but now it's time to learn a little more about how this statement actually works. This topic becomes important when you define your own collection classes, and this chapter describes how you can make collections enumerable.

# Enumerating the elements in a collection

Chapter 10 presents an example of using the foreach statement to list the items in a simple array. The code looks like this:

```
int[] pins = { 9, 3, 7, 2 };
foreach (int pin in pins)
{
    Console.WriteLine(pin);
}
```

The foreach construct provides an elegant mechanism that greatly simplifies the code you need to write, but it can be exercised only under certain circumstances: you can use foreach only to step through an enumerable collection. What exactly is an enumerable collection? The quick answer is that it's a collection that implements System.Collections.IEnumerable interface.

> Note
Remember that all arrays in C# are instances of the System.Array class. The System.Array class is a collection class that implements the IEnumerable interface.

The IEnumerable interface contains a single method called GetEnumerator:

```
IEnumerator GetEnumerator();
```

The GetEnumerator method should return an enumerator object that implements the System.Collections.IEnumerable interface. The enumerator object is used for stepping through (enumerating) the elements of the collection. The IEnumerable interface specifies the following property and methods:

```
object Current { get; }
bool MoveNext();
void Reset();
```

Think of an enumerator as a pointer indicating elements in a list. Initially, the pointer points before the first element. You call the MoveNext method to move the pointer down to the next (first) item in the list; the MoveNext method returns true if there's another item and false if isn't. Use the Current property to access the item currently pointed to, and you use the Reset method to return the pointer back to before the first item in the list. By using the GetEnumerator method of a collection to create an enumerator, repeatedly calling the MoveNext method, and using the enumerator to retrieve the value of the Current property, you can move forward through the elements of a collection one item at a time. This is exactly how the foreach statement does. So, if you want to create your own enumerable collection class, you must implement the IEnumerable interface in your collection class and provide an implementation of the IEnumerator interface to be returned by the GetEnumerator method of the collection class.

> **Important**
At glance, it's easy to confuse the IEnumerable and IEnumerator interfaces because their names are so similar. Be certain not to mix them up.

You might have noticed that the Current property of the IEnumerator exhibits non-safe behavior in it returns an object rather than a specific type. However, you should be pleased to know that the Microsoft .NET class library also provides the generic IEnumerator<T> interface, which has a Current property that returns a T instead. Likewise, there's IEnumerable<T> interface containing a GetEnumerator method that returns an Enumerator<T> object. Both of these interfaces are defined in the System.Collections.Generic namespace. If you're building applications for .NET version 2.0 or later, you should use these generic interfaces rather than the nongeric versions when you define enumerable collections.

# Manually implementing an enumerator

In the following exercise, you will define a class that implements the generic IEnumerator<T> interface and create an enumerator for the binary tree class demonstrated in Chapter 17, "Introducing generics."

Chapter 17 illustrates how easy it is to traverse a binary tree and display its contents. You would, therefore, be inclined to think that defining an enumerator retrieves each element in a binary tree in the same order would be a simple matter. Sadly, you would be mistaken. The main problem is when defining an enumerator, you must remember that you are in the structure that subsequent calls to the MoveNext method can update the position appropriately. Recursive algorithms, such as that used when walking a binary tree, do not lend themselves to maintaining state information between method calls in an easily accessible manner. For this reason, you will first preprocess the data in the binary tree into a more amenable data structure (a queue) and enumerate this data structure instead. Of course, this deviousness is hidden from the user iterating through the elements of the binary tree!

# To create the TreeEnumerator class

1. Start Microsoft Visual Studio 2022, if it is not already running.
2. Open the BinaryTree solution, which is located in the \Microsoft Press\VCSDB\Chapter19\BinaryTree folder in your Documents folder. This solution contains a working copy of the BinaryTree project you created in Chapter 17. You'll add a new class to project in which to implement the enumerator for the BinaryTree class.
3. In Solution Explorer, select the BinaryTree project. Then, open the Project menu and select Add to open the Add New Item – dialog.
4. In the middle pane, select the Class template, type TreeEnumerator.cs in the Name box, and then select Add. The TreeEnumerator will generate an enumerator for a Tree<TItem> object. To ensure that the class is safe, you must provide a type parameter and implement the IEnumerator<T> interface. Also, the type parameter must be a valid type for the Tree<TItem> object that the class enumerates, so it must be constrained to IComparable<TItem>. (The BinaryTree class requires that items in the tree provides a means to be compared for sorting purposes.)
5. In the Code and Editor window displaying the TreeEnumerator.cs file, modify the definition of the TreeEnumerator class to satisfy these requirements, as shown in bold in the following example:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
IComparable<TItem>
{
}
```

> Note
Visual Studio will display some warnings and error messages because the IEnumerator interface expects you to implement certain methods and properties that you haven't added. You'll define these items shortly, so you can ignore these messages.

6. Add the three private variables shown in bold in the following code to the TreeEnumerator<TItem> class:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
IComparable<TItem>
{
    private Tree<TItem> currentData = null;
    private Tree<TItem> currentItem = default(TItem);
    private Queue<TItem> enumData = null;
}
```

The currentData variable will be used to hold a reference to the tree enumerated, and the currentItem will hold the value returned by the Current property. You'll populate the enumData queue with the values extracted from the nodes in the tree, and the MoveNext method will return each item from this queue in turn.

> Note
The default keyword is explained in the sidebar titled “Initializing a variable defined with a type parameter” later in this section.

7. Add a constructor that takes a Tree<TItem> parameter data to the constructor, the TreeEnumerator<TItem> class. In the body of the constructor, add the statement shown in bold that initializes the currentData variable to data:
