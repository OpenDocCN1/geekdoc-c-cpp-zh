# EXTENDING CLOSED CLASSES

There's one last twist to working with classes in .NET: extension methods. EXTENSION METHODS behave as though they were standard instance methods, but they're defined in a separate class (and usually a separate namespace). They allow you to add new methods to a class without re-compiling or inheriting from it, so you can extend the functionality of sealed classes and classes, like those in the BCL, that you can't or shouldn't change directly. Let's look at how they work:

+   0 It isn't required, but you'll usually define your extension methods in a new namespace in order to simplify referencing them in your code. You'll usually call the namespace something like <Project>Extensions.

+   1 Declare a public static class to contain the methods.

+   2 Declare each method using the public static keywords as well.

+   3 The first parameter of the method must be the name of the class the method extends, preceded by the keyword this. You omit this parameter when you call the method in your code.

+   4 In the code that's going to use the extension method, reference the namespace you declared with the standard using <namespace>; syntax

+   6 You can call the method just as though it were an instance method. (Remember, you omit that first parameter specifying the class.)

![](bbox=[0.09, 0.66, 0.9, 0.88])