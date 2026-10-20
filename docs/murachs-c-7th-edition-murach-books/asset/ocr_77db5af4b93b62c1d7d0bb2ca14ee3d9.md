# How to work with namespaces

As you know, a namespace is a container that is used to group related classes. For example, all of the .NET classes that are used for creating Windows forms are grouped in the System.Windows.Forms namespace, and all of the classes for working with collections are grouped in the System.Collections namespace.

Every C# class you create must also belong to a namespace. This namespace is identified by a namespace statement that appears near the beginning of the C# source file. This is illustrated in all three of the examples in figure 16-3.

When you create a C# application, Visual Studio creates a namespace that has the same name as the project. Then, it stores all of the classes you create for that project in that namespace. For example, the default form for the Product Maintenance application is stored in a namespace named ProductMaintenance as shown in the first example in this figure. In addition, any other class you create as part of this project is stored in the same namespace.

You can also nest namespaces. In fact, most of the .NET namespaces are nested. For example, System.Collections is actually a namespace named Collections that’s nested within a namespace named System. As this figure shows, you can create nested namespaces using one of two techniques. First, you can code a namespace statement within another namespace as shown in the second example. This example creates a namespace named Murach.Validation. The more common technique, however, is to simply name all of the nested namespaces on a single namespace statement as shown in the third example.

Although all of the classes of a project are typically stored in the same namespace, those classes use classes that are stored in other namespaces. For example, all C# applications use classes that are defined by .NET. To use a class in another namespace, you typically include a using directive for that namespace at the beginning of the class. Alternatively, you can qualify any reference to the class with the name of the namespace.

For simple C# projects, you don’t need to worry about namespaces because Visual Studio takes care of them for you. However, namespaces may become an issue in two situations. The first situation occurs if you copy a class from one project into another project. When you do that, you may need to change the name of the namespace in the class file to the name of the namespace for the project you copied the class into.

The second situation occurs if you want to share a class among several projects by creating a class library. In that case, you should create a separate namespace for the classes in the library. You’ll learn how to do that later in this chapter.