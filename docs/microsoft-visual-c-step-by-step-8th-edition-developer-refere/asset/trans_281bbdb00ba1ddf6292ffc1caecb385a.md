

methods and adds them to the class. The nongeneric IEnumerable interface method is implemented because the generic IEnumerable<TItem> interface inherits from IEnumerable.

+   4. Locate the generic IEnumerable<TItem>.GetEnumerator method near the end of the class. Modify the body of the GetEnumerator() method, replacing the existing throw statement, as shown in bold in the following example:

Click here to view code image

```
IEnumerator<TItem> IEnumerable<TItem>.GetEnumerator()
{
    return new TreeEnumerator<TItem>(this);
}
```

The purpose of the GetEnumerator method is to construct an enumerator object for iterating through the collection. In this case, all you need to do is build a new TreeEnumerator<TItem> object by using the data in the tree.

+   5. Build the solution. Correct any errors that are reported, and rebuild the solution if necessary.

You will now test the modified Tree<TItem> class by using a foreach statement to iterate through a binary tree and display its contents.

## Test the enumerator

+   1. In Solution Explorer, right-click the BinaryTree solution, point to Add, and then click New Project. Add a new project by using the Console Application template. Name the project EnumeratorTest, set the location to \Microsoft Press\VCSBS\Chapter 19\BinaryTree in your Documents folder, and then click OK.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_509_0.png)

# Note

Be sure that you select the Console Application template from the list of Visual C# templates. Sometimes the Add New Project dialog box displays the templates for Visual Basic or C++ by default.

+   2. Right-click the EnumeratorTest project in Solution Explorer, and then click Set As StartUp Project.

+   3. On the Project menu, click Add Reference. In the Reference Manager – EnumeratorTest dialog box, in the left pane, expand the Projects node and click Solution. In the middle pane, select the BinaryTree project, and then click OK.

The BinaryTree assembly appears in the list of references for the EnumeratorTest project in Solution Explorer.

4. In the Code and Text Editor window displaying the Program class, add the following using directive to the list at the top of the file:

```
using BinaryTree;
```

5. Add to the Main method the statements shown in bold in the code that follows. These statements create and populate a binary tree of integers:

Click here to view code image

```
static void Main(string[] args)
{
    Tree<int> tree1 = new Tree<int>(10);
    tree1.Insert(5);
    tree1.Insert(11);
    tree1.Insert(5);
    tree1.Insert(-12);
    tree1.Insert(15);
    tree1.Insert(0);
    tree1.Insert(14);
    tree1.Insert(-8);
    tree1.Insert(10);
}
```

6. Add a foreach statement, as follows in bold, that enumerates the contents of the tree and displays the results:

Click here to view code image

```
static void Main(string[] args)
{
    ...
    foreach (int item in tree1)
    {
        Console.WriteLine(item);
    }
}
```

7. On the Debug menu, click Start Without Debugging.

The program runs and displays the values in the following sequence:
−12, −8, 0, 5, 5, 10, 10, 11, 14, 15

![](img/16f6e3fe08f01ddadb2741a92c392b0e_510_0.png)

8. Press Enter to return to Visual Studio 2015.

## Implementing an enumerator by using an iterator

As you can see, the process of making a collection enumerable can become complex and is potentially prone to error. To make life easier, C# provides iterators that can automate much of this process.

An iterator is a block of code that yields an ordered sequence of values. An iterator is not actually a member of an enumerable class; rather, it specifies the sequence that an enumerator should use for returning its values. In other words, an iterator is just a description of the enumeration sequence that the C# compiler can use for creating its own enumerator. This concept requires a little thought to understand properly, so consider the following simple example.

### A simple iterator

The following BasicCollection<T> class illustrates the principles of implementing an iterator. The class uses a List<T> object for holding data and provides the FillList method for populating this list. Notice also that the BasicCollection<T> class implements the IEnumerable<T> interface. The GetEnumerator method is implemented by using an iterator:

Click here to view code image

```
using System;
using System.Collections.Generic;
using System.Collections;

class BasicCollection<T> : IEnumerable<T>
{
    private List<T> data = new List<T>();

    public void FillList(params T [] items)
    {
        foreach (var datum in items)
        {
            data.Add(datum);
        }
    }

    IEnumerator<T> IEnumerable<T>.GetEnumerator()
    {
        foreach (var datum in data)
        {
            yield return datum;
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        // Not implemented in this example
        throw new NotImplementedException();
```

The GetEnumerator method appears to be straightforward, but it warrants closer examination. The first thing to notice is that it doesn’t appear to return an IEnumerator<T> type. Instead, it loops through the items in the data array, returning each item in turn. The key point is the use of the yield keyword. The yield keyword indicates the value that should be returned by each iteration. If it helps, you can think of the yield statement as calling a temporary halt to the method, passing back a value to the caller. When the caller needs the next value, the GetEnumerator method continues at the point at which it left off, looping around and then yielding the next value. Eventually, the data is exhausted, the loop finishes, and the GetEnumerator method terminates. At this point, the iteration is complete.

Remember that this is not a normal method in the usual sense. The code in the GetEnumerator method defines an iterator. The compiler uses this code to generate an implementation of the IEnumerator<T> class containing a Current method and a MoveNext method. This implementation exactly matches the functionality specified by the GetEnumerator method. You don’t actually get to see this generated code (unless you decompile the assembly containing the compiled code), but that is a small price to pay for the convenience and reduction in code that you need to write. You can invoke the enumerator generated by the iterator in the usual manner, as shown in the following block of code, which displays the words in the first line of the poem “Jabberwocky” by Lewis Carroll:

Click here to view code image

```
BasicCollection<string> bc = new BasicCollection<string>();
bc.FillList("Twas", "brillig", "and", "the", "slithy", "toves");
foreach (string word in bc)
{
    Console.WriteLine(word);
}
```

This code simply outputs the contents of the bc object in this order:

Twas, brillig, and, the, slithy, toves

If you want to provide alternative iteration mechanisms to present the data in a different sequence, you can implement additional properties that implement the IEnumerable interface and that use an iterator for returning data. For example, the Reverse property of the BasicCollection<T> class, shown here, emits the data in the list in reverse order:

Click here to view code image

```
class BasicCollection<T> : IEnumerable<T>
{
    ...
    public IEnumerable<T> Reverse
```

```
{
    get
    {
        for (int i = data.Count - 1; i >= 0; i--)
        {
            yield return data[i];
        }
    }
}
```

You can invoke this property as follows:

Click here to view code image

```
BasicCollection<string> bc = new BasicCollection<string>();
bc.FillList("Twas", "brillig", "and", "the", "slithy", "toves");
foreach (string word in bc.Reverse)
{
    Console.WriteLine(word);
}
```

This code outputs the contents of the bc object in reverse order:

toves, slithy, the, and, brillig, Twas

## Defining an enumerator for the Tree<TItem> class by using an iterator

In the next exercise, you will implement the enumerator for the Tree<TItem> class by using an iterator. Unlike in the preceding set of exercises, which required the data in the tree to be preprocessed into a queue by the MoveNext method, here you can define an iterator that traverses the tree by using the more naturally recursive mechanism, similar to the WalkTree method discussed in Chapter 17.

## Add an enumerator to the Tree<TItem> class

+   1. Using Visual Studio 2015, open the BinaryTree solution, located in the \Microsoft Press\VCSBS\Chapter 19\IteratorBinaryTree folder in your Documents folder. This solution contains another copy of the BinaryTree project you created in Chapter 17.

+   2. Open the file Tree.cs in the Code and Text Editor window. Modify the definition of the Tree<TItem> class so that it implements the IEnumerable<TItem> interface, as shown here in bold:

Click here to view code image

```
public class Tree<TItem> : IEnumerable<TItem> where TItem :
IComparable<TItem>
{
    ...
}
```

+   3. Hover over the IEnumerable<TItem> interface in the class definition. On

