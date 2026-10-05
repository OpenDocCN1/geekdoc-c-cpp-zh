```
Console.WriteLine("Sorted data is: {sortedData}");
}
```

These statements create a new binary tree for holding ints. The constructor creates an initial node containing the value 10. The Insert statements add nodes to the tree

> Remember that the int keyword in C# is just an alias for the System.Int32 type. Whenever you declare an int variable, you're actually declaring a struct variable of type System.Int32. The System.Int32 implements IComparable and IComparable<T> interfaces, Similarly, the string keyword is an alias for System.String, which also implements IComparable and IComparable<T>.

+   8. On the Build menu, select Build Solution. Correct any errors if necessary.

+   9. On the Debug menu, select Start Without Debugging.

Verify that the program runs and displays the values in the following sequence:

Click here to view code image

-12 -8 0 5 5 8 10 11 14 15

+   10. Press Enter to return to Visual Studio 2022.

+   11. Add the following statements shown in bold to the end of the Main method in the existing code:

Click here to view code image

```
static void Main(string[] args)
{
    ...
    Tree<string> tree2 = new Tree<string>("Hello");
```