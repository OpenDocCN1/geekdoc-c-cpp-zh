![](bbox=[0.176, 0.113, 0.811, 0.274])

**Fig. 15.45** | Base Form for use with visual inheritance. (Part 2 of 2.)

# Steps for Declaring and Using a Reusable Class

Before a Form (or any class) can be used in multiple apps, it must be placed in a class library to make it reusable. The steps for creating a reusable class are:

+   1. Declare a public class. If the class is not public, it can be used only by other classes in the same assembly—that is, compiled into the same DLL or EXE file.
+   2. Choose a namespace name and add a namespace declaration to the source-code file for the reusable class declaration.
+   3. Compile the class into a class library.
+   4. Add a reference to the class library in an app.
+   5. Use the class.

Let’s take a look at these steps in the context of this example:

# Step 1: Creating a public Class

For Step 1 in this discussion, we use the public class VisualInheritanceBaseForm declared in Fig. 15.45. By default, every new Form class you create is declared as a public class.

# Step 2: Adding the namespace Declaration

For Step 2, we use the namespace declaration that was created for us by the IDE. By default, every new class you define is placed in a namespace with the same name as the project. In almost every example in the text, we’ve seen that classes from preexisting libraries, such as the .NET Framework Class Library, can be imported into a C# app. Each class belongs to a namespace that contains a group of related classes. As apps become more complex, namespaces help you manage the complexity of app components. Class libraries and namespaces also facilitate software reuse by enabling apps to add classes from other namespaces (as we’ve done in many examples). We removed the namespace declarations in earlier chapters because they were not necessary.

Placing a class inside a namespace declaration indicates that the class is part of the specified namespace. The namespace name is part of the fully qualified class name, so the name of class VisualInheritanceTestForm is actually VisualInheritanceBase.VisualInheritanceBaseForm. You can use this fully qualified name in your apps, or you can write a using directive and use the class’s simple name (the unqualified class name—VisualInheritanceBaseForm) in the app. If another namespace also contains a class with the