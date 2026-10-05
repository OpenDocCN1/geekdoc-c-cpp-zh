# How to create and use class libraries

So far, the classes you've seen have been created as part of a Windows Forms Application project. If you want to be able to use the classes you create in two or more projects, however, you'll want to store them in class libraries. Simply put, a class library consists of a collection of related classes. When you use a class library, you can use any of the classes in the library without copying them into the project.

# Class libraries work

Figure 16-6 illustrates the difference between using classes within a Windows Forms Application project and classes created within a class library project. As you can see, classes that are created in a Windows project must be included in every project that uses them. In contrast, classes that are created in a class library exist separately from any project that uses them. Because of that, they are available to any project that has access to the class library.

One of the benefits of using class libraries is that the size of each project that uses the class library rather than the code for each class it needs. Also, because the classes in a class library are already compiled, Visual Studio doesn't have to compile them every time you build the application. This results in faster compile times.

Another benefit of using class libraries is that they simplify maintenance. If you must make a change to a class that's in a class library, you can change the class without changing any of the applications that use the library. When you're done, the modified library is immediately available to the projects that use it.

But the mainly benefit of using class libraries is that they let you create reusable code. If you design your classes carefully and place them in a library, you can reuse them in other projects that require similar functions. In most cases, you'll use the classes directly. However, you can also use them as base classes for the new classes that you add to your projects.