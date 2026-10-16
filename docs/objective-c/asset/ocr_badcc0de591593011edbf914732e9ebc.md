# Including the headers

Remember that simply linking with the framework is not enough to enable you to actually use the classes and code contained within it. You also need to be sure to include the appropriate header files into your source file. Recall when you learned about importing header files that you tell the compiler to search the linked framework directories by enclosing the name of the header file you are importing in <>. Doing so causes the compiler to search the system including directories as well as any framework directories.

# Considering garbage collection

An important consideration when linking with third-party frameworks is to ensure that the framework in question supports the memory management model that you have selected for your project. Not all frameworks support both garbage collection and reference counted memory management. So be sure when you are reviewing the documentation for the framework that you intend to link to your project that you are linking with the correct version of that framework for the memory management system that you have selected. Linking with the incorrect version will cause a compilation error.

# Summary

In this chapter, I have introduced you to the concept of frameworks and also talked about the Foundation framework which serves as the closest thing to a standard library that Objective-C has. The remainder of this part of the book will utilize the Foundation framework extensively and it is important that you have this conceptual introduction to the framework and what it provides. Now that you have this background information, you’ll be better prepared for the detailed coding examples to come.