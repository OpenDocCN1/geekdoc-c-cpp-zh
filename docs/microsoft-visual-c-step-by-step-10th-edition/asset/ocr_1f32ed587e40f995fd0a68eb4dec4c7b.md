# Defining a generic method to build a binary tree

In the previous exercise, you created a generic class for implementing a binary tree. The Tree<Item> class provides the Insert method for adding data items to the tree. However, if you want to add a large number of items, repeated calls to the Insert method are not very convenient. In the following exercise, you'll define a generic method called InsertIntoTree that you can use to insert a list of data items into a tree with a single method call. You'll test this method by using it to insert a list of characters into a tree of characters.

# To write the InsertIntoTree method

+   1. In Visual Studio 2022, on the File menu, select Close Solution. Save the solution if prompted.

+   2. Create a new project using the Console Application template. Set the location to \Microsoft Press\VCSBS\Chapter17 in your Documents folder, and select the .NET 6.0 framework.

+   3. On the Project menu, select Add Project Reference.

+   4. In the Reference Manager – BuildTree dialog, select the Browse button (not the Browse tab in the left pane),

+   5. In the Select files to reference dialog, browse to the folder MicrosoftPress\VCSBS\Chapter17\BinaryTree\bin\Debug\net6.0 in your Documents folder, select BinaryTree.dll, and then select Add.

+   6. In the Reference Manager – BuildTree dialog, verify that the BinaryTree.dll is listed and that the checkbox for this is selected, and then select OK.

+   7. In the Solution Explorer window, expand Dependencies, and then expand Assemblies. Verify that the BinaryTree assembly has been added to the list of references for the project.