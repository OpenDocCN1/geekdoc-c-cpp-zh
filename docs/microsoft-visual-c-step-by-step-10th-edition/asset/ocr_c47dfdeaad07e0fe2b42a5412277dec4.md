reason, you will first preprocess the data in the binary tree into a more amenable data structure (a queue) and enumerate this data structure instead. Of course, this deviousness is hidden from the user iterating through the elements of the binary tree!

# To create the TreeEnumerator class

+   1. Start Microsoft Visual Studio 2022, if it is not already running.
2. Open the BinaryTree solution, which is located in the \Microsoft Press\VCSDB\Chapter19\BinaryTree folder in your Documents folder. This solution contains a working copy of the BinaryTree project you created in Chapter 17. You'll add a new class to project in which to implement the enumerator for the BinaryTree class.
3. In Solution Explorer, select the BinaryTree project. Then, open the Project menu and select Add Class to open the Add New Item – Binary dialog.
4. In the middle pane, select the Class template, type TreeEnumerator.cs in the Name box, and then select Add.

The TreeEnumerator will generate an enumerator for a Tree<TItem> object. To ensure that the class is safe, you must provide a type parameter and implement the IEnumerator<T> interface. Also, the type parameter must be a valid type for the Tree<TItem> object that the class enumerates, so it must be constrained to implement IComparable<TItem> interface. (The BinaryTree class requires that items in the tree provides a means to be compared for sorting purposes.)

5. In the Code and Text Editor window displaying the TreeEnumerator.cs file, modify the definition of the TreeEnumerator class to satisfy these requirements, as shown in bold in the following example:

Click here to view code image

```
class TreeEnumerator<TItem> : IEnumerator<TItem> where TItem :
IComparable<TItem>
{
}
```