```
return 1;

    return -1;
  }
}
```

The parameter for the CompareTo method must match the type specified in the interface, IComparable<Circle>. In general, it is preferable to implement the System.IComparable<T> interface rather than the System.IComparable interface. You can also implement both, just as many of the types in the .NET Framework do.

# Create the Tree<TItem> class

+   1. Start Microsoft Visual Studio 2015 if it is not already running.
+   2. On the File menu, point to New, and then click Project.
+   3. In the New Project dialog box, in the Templates pane on the left, click Visual C#. In the middle pane, select the Class Library template. In the Name box, type BinaryTree. In the Location box, specify \Microsoft Press\VCSBS\Chapter 17 in your Documents folder, and then click OK.

# Note

Using the Class Library template, you can create assemblies that can be used by multiple applications. To use a class in a class library in an application, you must first copy the assembly containing the compiled code for the class library to your computer (if you did not create it yourself) and then add a reference to this assembly.

+   4. In Solution Explorer, right-click Class1.cs, click Rename, and then change the name of the file to Tree.cs. Allow Visual Studio to change the name of the class as well as the name of the file when you are prompted.
+   5. In the Code and Text Editor window, change the definition of the Tree class to Tree<TItem>, as shown in bold in the following code:

```
public class Tree<TItem>
{
}
```

6. In the Code and Text Editor window, modify the definition of the Tree<TItem> class to specify that the type parameter TItem must denote a type that implements the generic IComparable<TItem> interface. The changes are highlighted in bold in the code example that follows.
The modified definition of the Tree<TItem> class should look like this: