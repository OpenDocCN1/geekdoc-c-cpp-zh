# Chapter 20. Decoupling application logic and handling events

After completing this chapter, you will be able to:

+   - Declare a delegate type to create an abstraction of a method signature.
+   - Create an instance of a delegate to refer to a specific method.
+   - Call a method through a delegate.
+   - Define a lambda expression to specify the code to be executed by a delegate.
+   - Declare an event field.
+   - Handle an event by using a delegate.
+   - Raise an event.

Many of the examples and exercises in this book have placed great emphasis on the careful definition of classes and structures to enforce encapsulation. In this way, the implementation of the methods in these types can change without unduly affecting the applications that use them. Sometimes, however, it is not possible or desirable to encapsulate the entire functionality of a type. For example, the logic for a method in a class might depend upon which component or application invokes this method, which might need to perform some application or component-specific processing as part of its operation. However, when you build such a class and implement its methods, you might not know which applications and components are going to use it, and you need to avoid introducing dependencies in your code that might restrict the use of your class. Delegates provide the ideal solution, making it possible for you to fully decouple the application logic in your methods from the applications that invoke them.

Events in C# support a related scenario. Much of the code you have written in the exercises in this book assumes that statements execute sequentially. Although this is the most common case, you will find that it is sometimes necessary to interrupt the current flow of execution to perform another, more important task. When that task is complete, the program can continue where it left off. The classic examples of this style of program are the Universal Windows Platform (UWP) forms that you have been using in the exercises involving graphical applications. A form displays controls such as buttons and text boxes. When you click a button or type text in a text box, you expect the form to respond immediately. The application has to temporarily stop what it is doing and handle your input. This style of operation applies not only to graphical user interfaces (GUIs), but also to any application where an operation must be performed urgently—shutting down the reactor in a nuclear power plant if it is getting too hot, for example. To handle this kind of processing, the runtime has to provide two things: a means of