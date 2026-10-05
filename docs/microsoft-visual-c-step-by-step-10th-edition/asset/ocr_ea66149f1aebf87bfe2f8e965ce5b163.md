# Create a new project

Recent project templates

+   - Console Application
- Blank App (Universal Windows)
- Class Library
- Class Library (Universal Windows)

![](bbox=[0.405, 0.11, 0.835, 0.465])

4. In the Configure your new project dialog, in the **Project name** box, type **BinaryTree**. In the **Location** box, specify `\Microsoft Press\VCSB\Chapter 17` in your **Documents** folder. Then select **Next.**

5. In the Additional information dialog, select the framework to **.NET 6.0**, and then select **Create.**

Using the Class Library template, you can create assemblies that can be reused by different applications. To use a class in a class library in an application, you must first copy the assembly containing the compiled code for the class library to your computer (if you didn't create it yourself) and then add a reference to this assembly.

6. In Solution Explorer, right-click **Class.cs**, select **Rename**, and change the name of the file to **Tree.cs**. Allow Visual Studio to change the name of the class as well as the name of the file when you're prompted.

7. In the Code and Text Editor window, change the definition of the *Tree* class to `Tree<TItem>`, as shown in the following code: