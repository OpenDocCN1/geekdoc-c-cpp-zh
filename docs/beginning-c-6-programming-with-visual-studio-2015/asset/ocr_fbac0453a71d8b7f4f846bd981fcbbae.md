+   - Classes implementing interfaces have lollipops.
+   - Abstract classes are shown with a dotted outline and italicized name.
+   - Sealed classes are shown with a thick black outline.

Clicking on an object shows you additional information in a Class Details window at the bottom of the screen (right-click an object and select Class Details if this window doesn't appear). Here, you can see (and modify) class members. You can also modify class details in the Properties window.

From the Toolbox, you can add new items such as classes, interfaces, and enums to the diagram, and define relationships between objects in the diagram. When you do this, the code for the new items is automatically generated for you.

# CLASS LIBRARY PROJECTS

As well as placing classes in separate files within your project, you can also place them in completely separate projects. A project that contains nothing but classes (along with other relevant type definitions, but no entry point) is called a class library.

Class library projects compile into .dll assemblies, and you can access their contents by adding references to them from other projects (which might be part of the same solution, but don't have to be). This extends the encapsulation that objects provide because class libraries can be revised and updated without touching the projects that use them. That means you can easily upgrade services provided by classes (which might affect multiple consumer applications).

The following Try It Out provides an example of a class library project and a separate project that makes use of the classes that it contains.

# TRY IT OUT Using a Class Library: Ch09ClassLib and Ch09Ex02\Program.cs

+   1. Create a new project of type Class Library called Ch09ClassLib and save it in the directory c:\BegVCSharp\Chapter09, as shown in Figure 9-7.
+   2. Rename the file Class1.cs to MyExternalClass.cs (by right-clicking on the file in the Solution Explorer window and selecting Rename). Click Yes on the dialog box that appears.
+   3. The code in MyExternalClass.cs automatically changes to reflect the class name change:
+   4. Add a new class to the project, using the filename MyInternalClass.cs.
+   5. Modify the code to make the class MyInternalClass explicitly internal:
+   6. Compile the project (this project has no entry point, so you can't run it as normal — instead, you can build it by selecting Build ➔ Build Solution).

```
public class MyExternalClass
{
}
```

```
internal class MyInternalClass
{
}
```