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

# Test the enumerator

+   1. In Solution Explorer, right-click the BinaryTree solution, point to Add, and then click New Project. Add a new project by using the Console Application template. Name the project EnumeratorTest, set the location to \Microsoft Press\VCSBS\Chapter 19\BinaryTree in your Documents folder, and then click OK.

![](bbox=[0.105, 0.635, 0.165, 0.685])

# Note

Be sure that you select the Console Application template from the list of Visual C# templates. Sometimes the Add New Project dialog box displays the templates for Visual Basic or C++ by default.

+   2. Right-click the EnumeratorTest project in Solution Explorer, and then click Set As StartUp Project.

+   3. On the Project menu, click Add Reference. In the Reference Manager – EnumeratorTest dialog box, in the left pane, expand the Projects node and click Solution. In the middle pane, select the BinaryTree project, and then click OK.

The BinaryTree assembly appears in the list of references for the