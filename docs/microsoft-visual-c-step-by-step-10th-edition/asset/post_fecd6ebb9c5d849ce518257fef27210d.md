
your Documents folder. This solution contains another copy of the BinaryTree project you created in Chapter 17.

- 2. Open the file Tree.cs in the Code and Text Editor window. Then modify the definition of the TreeTItem class so that it implements the IEnumerable<TItem> interface, as shown here in bold:

Click here to view code image

```csharp
public class Tree<TItem> : IEnumerable<TItem> where TItem :
IComparable<TItem>
{
  ...
}
```

- 3. Hover over the IEnumerable<TItem> interface in the class definition. On the dropdown context menu that appears, select Implement all members explicitly to add the IEnumerable<TItem>.GetEnumerator methods to the end of the class.

- 4. Locate the generic IEnumerable<TItem>.GetEnumerator method. Replace the contents of the GetEnumerator method as shown in bold in the following code:

Click here to view code image

```csharp
IEnumerable<TItem> IEnumerable<TItem>.GetEnumerator()
{
  if (this.LeftTree is not null)
  {
    foreach (TItem item in this.LeftTree)
    {
      yield return item;
    }
  }
  yield return this.NodeData;

  if (this.RightTree is not null)
  {
    foreach (TItem item in this.RightTree)
    {
      yield return item;
    }
  }
```

# To test the new enumerator

- 1. In Solution Explorer, right-click the **BinaryTree** solution, point to **Add**, and then select **Existing Project**.
- 2. In the Add Existing Project dialog, move to the folder \Microsoft Press\VCSB\Chapter 19\BinaryTree\EnumeratorTest, select the **EnumeratorTest** project file, and then select **Open**.
This is the project that you created to test the enumerator you developed manually earlier in this chapter.
- 3. Right-click the **EnumeratorTest** project in Solution Explorer, and then select **Set As Startup Project**.
- 4. In Solution Explorer, expand the **Dependencies** folder for the **EnumeratorTest** project, and then expand the **Projects** folder. Right-click the **BinaryTree** reference and then select **Remove**.
- 5. On the **Project** menu, select **Add Project Reference**.
- 6. In the left pane of the Reference Manager – EnumeratorTest dialog, expand the **Projects** node and select **Solution**. In the middle pane, select the **BinaryTree** project. Then select **OK**.

It might not be obvious at first glance, but this code follows the same recursive algorithm that you used in Chapter 17 to list the contents of a binary tree. If `LeftTree` is not empty, the first `foreach` statement implicitly calls the `Enumerator` method (which you are currently defining). This process continues until a node has no left subtree. At this point, the value in the `NodeData` property is yielded, and the right subtree is exhausted, the process unwinds to the parent node, outputting the parent’s `NodeData` property and examining the right subtree of the parent. This course of action continues until the entire tree has been enumerated and all the nodes have been output.

These three steps ensure that the EnumeratorTest project references the correct version of the BinaryTree assembly. It should use the assembly that implements the enumerator by using the iterator rather than the version created in the previous set of exercises in this chapter.

- Display the Program.cs file for the EnumeratorTest project in the Code and Text Editor window.

- Review the Main method in the Program.cs file. Recall from testing the earlier enumerator that this method instantiates a Tree<int> object, fills it with some data, and then uses a foreach statement to display its contents.

- Build the solution and correct any errors if necessary.

- On the Debug menu, select Start Without Debugging.

The program runs and displays the values in the same sequence as before.

Click here to view code image

```
-12, -8, 0, 5, 5, 10, 11, 14, 15
```

- Press Enter and return to Visual Studio 2022.

# Summary

In this chapter, you saw how to implement the IEnumerable<T> and IEnumerator<T> interfaces with a collection class to enable applications to iterate through the items in the collection. You also saw how to implement enumerator by using an iterator.

- If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 20, “Decoupling application logic and handling events."

- If you want to exit Visual Studio 2022 now, on the File menu, select Exit.
If you see a Save dialog, select Yes and save the project.

# Quick reference

| To | Do this |
| --- | --- |
| Make a collection class enumerable, allowing it to support the foreach construct | Implement the IEnumerable interface and provide a GetEnumerator method that returns an IEnumerator. For example:
Click here to view code image
```csharp
public class Tree<TItem> :
  IEnumerable<TItem>
{
  IEnumerable<TItem> GetEnumerator()
  {
    ...
  }
}
``` |
| Implement an enumerator without using an iterator | Define an enumerator class that implements the IEnumerable interface and provides the Current property and the MoveNext method (and optionally the Reset method). For example:
Click here to view code image
```csharp
public class TreeEnumerator<TItem> :
  IEnumerable<TItem>
{
  TItem Current
  {
    get
    ...
  }
}
``` |

```csharp
bool MoveNext()
{
  ...
}
```

Define an enumerator by using an iterator

Implement the enumerator to indicate which items should be returned (using the yield statement) and in which order. For example:

Click here to view code image

```csharp
IEnumerator<TItem> GetEnumerator()
{
  for (...)
{
    yield return ...
  }
}
```

Chapter 20

# Decoupling application logic and handling events

After completing this chapter, you will be able to:

- Declare a delegate type to create an abstraction of a method signature, and call a method through a delegate.
- Define a lambda expression to specify the code to be executed by a delegate.
- Enable notifications by using events.
- Understand how the Windows user interface utilizes events to handle user interactions.
- Handle an event by using a delegate.

Many of the examples and exercises in this book have placed great emphasis on the careful definition of classes and structures to enforce encapsulation. In this way, the implementation of the methods in these types can change without unduly affecting the applications that use them. Sometimes, however, it's not possible or desirable to encapsulate the entire functionality of a type. For example, the logic for a method in a class might depend upon which component or application invokes the method, which might need to perform some application or component-specific processing as part of its operation. However, when you build such a class and implement its methods, you might not know which applications and components will use it, and you need to avoid introducing dependencies in code that might restrict the use of your class. Delegates provide the ideal solution, making it possible for you to fully decouple the application logic in your methods from the applications that invoke them.

Events in C# support a related scenario. Much of the code you've written in the exercises in this book assumes that statements execute sequentially. Although this is the most common case, you'll find that it is sometimes necessary to interrupt the normal flow of execution to perform another. When that task is complete, the program can continue where it left off.

The classic examples of this style of program are the Universal Windows Platform (UWP) forms that you've been using in the exercises involving graphical applications. A form displays controls such as boxes and buttons. When you click a button or type in a box, you expect the form to respond immediately—meaning the application must temporarily stop what it's doing to handle your input. This style of operation applies not only to graphical user interfaces (GUIs) but also to any application where an operation must be performed urgently—shutting down the reactor in a nuclear power plant if it is getting too hot, for example.

To handle this kind of processing, the runtime must provide two things: a means of indicating that something has happened, and a way of specifying the code that should be run when the urgent event happens. Events, with delegates, provide the infrastructure with which you can implement systems that follow this approach.

# Understanding delegates

A delegate is a reference to a method. Delegates are so named because “delegate” processing to the referenced method when they are invoked. A delegate is a very simple concept with extraordinarily powerful implications. They explain me.

Typically, when you write a statement that invokes a method, you specify the name of the method (and possibly the object or structure to which the method belongs). It's clear from your code exactly which method you're running and when you are running. Look at the following simple example that calls the performCalculation method of a Processor object (what this method does or how the Processor class is defined is immaterial for this discussion):

```
Processor p = new Processor();
p.performCalculation();
```

You can assign a reference to a delegate in much the same way that you can assign an int value to an int variable. The next example creates a delegate named performDelegate references the performCalculation method of the Processor object. I have deliberately omitted some elements of the statement that declares the delegate because it's more important to understand the concept than to worry about the syntax. (You'll see the full syntax shortly.)
