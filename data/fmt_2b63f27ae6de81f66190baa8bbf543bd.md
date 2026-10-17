
The `Insert` method implements the recursive algorithm described earlier for creating an ordered binary tree. The constructor creates the initial node of the tree, so the `Insert` method can assume that the tree is not empty. The code that follows is the part of the algorithm that runs after checking whether the tree is empty. It’s reproduced here to help you understand the code you will write for the `Insert` method in the following steps:

Click here to view code image

```
...
Examine the value of the node, N, of the tree, B
If the value of N is greater than that of the new item, I
Then
    If the left subtree of B is empty
    Then
        Construct a new left subtree of B with the item I as the node, and empty left and right subtrees
    Else
        Insert I into the left subtree of B
End If
...
```

### 10. In the `Insert` method, add a statement that declares a local variable of type `TItem`, called `currentNodeValue`. Initialize this variable to the value of the `NodeData` property of the tree, as shown in bold in the following example:

Click here to view code image

```
public void Insert(TItem newItem)
{
    TItem currentNodeValue = this.NodeData;
}
```

### 11. Add the if-else statement shown in bold in the following code to the `Insert` method after the definition of the `currentNodeValue` variable.

This statement uses the `CompareTo` method of the `IComparable<T>` interface to determine whether the value of the current node is greater than that of the new item:

Click here to view code image

```
public void Insert(TItem newItem)
{
    TItem currentNodeValue = this.NodeData;
    if (currentNodeValue.CompareTo(newItem) > 0)
    {
        // Insert the new item into the left subtree
    }
}
```

```
else
{
    // Insert the new item into the right subtree
}
```

### 12. In the if part of the code, immediately after the comment // Insert the new item into the left subtree, add the following statements:

Click here to view code image

```
if (this.LeftTree == null)
{
    this.LeftTree = new Tree<TItem>(newItem);
}
else
{
    this.LeftTree.Insert(newItem);
}
```

These statements check whether the left subtree is empty. If so, a new tree is created using the new item and it is attached as the left subtree of the current node; otherwise, the new item is inserted into the existing left subtree by calling the `Insert` method recursively.

### 13. In the else part of the outermost if-else statement, immediately after the comment // Insert the new item into the right subtree, add the equivalent code that inserts the new node into the right subtree:

Click here to view code image

```
if (this.RightTree == null)
{
    this.RightTree = new Tree<TItem>(newItem);
}
else
{
    this.RightTree.Insert(newItem);
}
```

### 14. Add another public method called `WalkTree` to the `Tree<TItem>` class after the `Insert` method.

This method walks through the tree, visiting each node in sequence, and generates a string representation of the data that the tree contains. The method definition should look like this:

```
public string WalkTree()
{
}
```

### 15. Add to the `WalkTree` method the statements shown in bold in the code that follows.

These statements implement the algorithm described earlier for traversing a

binary tree. As each node is visited, the node value is returned by the method to the string:

Click here to view code image

```
public string WalkTree()
{
    string result = "";

    if (this.LeftTree != null)
    {
        result = this.LeftTree.WalkTree();
    }

    result += $" {this.NodeData.ToString()} ";

    if (this.RightTree != null)
    {
        result += this.RightTree.WalkTree();
    }

    return result;
}
```

### 16. On the Build menu, click Build Solution. The class should compile cleanly, but correct any errors that are reported and rebuild the solution if necessary.

In the next exercise, you will test the `Tree<TItem>` class by creating binary trees of integers and strings.

## Test the Tree<TItem> class

+ 1. In Solution Explorer, right-click the BinaryTree solution, point to Add, and then click New Project.

Note

Be sure that you right-click the BinaryTree solution rather than the BinaryTree project.

+ 2. Add a new project by using the Console Application template. Give the project the name `BinaryTreeTest`. Set the location to `\Microsoft Press\VCSBS\Chapter 17` in your Documents folder, and then click OK.

Note

A Visual Studio 2015 solution can contain more than one project. You are using this feature to add a second project to the BinaryTree solution for testing the `Tree<TItem>` class.

3. In Solution Explorer, right-click the `BinaryTreeTest` project, and then click Set As Startup Project.

The `BinaryTreeTest` project is highlighted in Solution Explorer. When you run the application, this is the project that will actually execute.

4. In Solution Explorer, right-click the `BinaryTreeTest` project, point to Add, and then click Reference.

5. In the left pane of the Reference Manager – BinaryTreeTest dialog box, expand Projects and then click Solution. In the middle pane, select the BinaryTree project (be sure to select the check box and not simply click the assembly), and then click OK.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_460_0.png)

This step adds the BinaryTree assembly to the list of references for the `BinaryTreeTest` project in Solution Explorer. If you examine the References folder for the `BinaryTreeTest` project in Solution Explorer, you should see the BinaryTree assembly listed at the top. You will now be able to create `Tree<TItem>` objects in the `BinaryTreeTest` project.

## Note

If the class library project is not part of the same solution as the project that uses it, you must add a reference to the assembly (the `.dll` file) and not to the class library project. You can do this by browsing for the assembly in the Reference Manager dialog box. You will use this technique in the final set of exercises in this chapter.

+ 6. In the Code and Text Editor window displaying the Program class in the `Program.cs` file, add the following using directive to the list at the top of the class:

+ 

+     `using BinaryTree;`

+ 7. Add to the `Main` method the statements shown in bold in the following code:

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
    tree1.Insert(8);
    tree1.Insert(8);

    string sortedData = tree1.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
```

These statements create a new binary tree for holding ints. The constructor creates an initial node containing the value 10. The `Insert` statements add nodes to the tree, and the `WalkTree` method generates a string representing the contents of the tree, which should appear sorted in ascending order when this string is displayed.

## Note

Remember that the `int` keyword in C# is just an alias for the `System.Int32` type; whenever you declare an `int` variable, you are actually declaring a struct variable of type `System.Int32`. The `System.Int32` type implements the `IComparable` and `IComparable<T>` interfaces, which is why you can create `Tree<int>` objects. Similarly, the `string` keyword is an alias for `System.String`, which also implements `IComparable` and `IComparable<T>`.

+ 8. On the Build menu, click Build Solution, and verify that the solution compiles. Correct any errors if necessary.

+ 9. On the Debug menu, click Start Without Debugging.

+ Verify that the program runs and displays the values in the following sequence:

+ −12 −8 0 5 5 8 8 10 10 11 14 15

+ 10. Press the Enter key to return to Visual Studio 2015.

+ 11. Add the following statements shown in bold to the end of the `Main` method in the `Program` class, after the existing code:

Click here to view code image
