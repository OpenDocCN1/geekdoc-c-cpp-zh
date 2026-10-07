# Object Oriented Programming using C#

Although the idea of structurally improving existing software is not new, the difference is as follows. In traditional development it was seen as a remedial action taken when the software design quality had degraded, usually as a result of phases of functional modification and extension. In agile methodologies refactoring is regarded as a natural healthy part of the development process.

# 10.3 Examples of Refactoring

During the development process a programmer may realise that a variable within a program has been badly named. However changing this is not a trivial task.

Changing a local variable will only require changes in one particular method – if a variable with the same name exists in a different method this will not require changing.

Thus implementing a seemingly trivial change requires an understanding of the consequences of that change.

Other complex changes may also be required. These include..

+   * Renaming an identifier everywhere it occurs
* Moving a method from one class to another
* Splitting code from one method into a separate method
* Changing the parameter list of a method
* Rearranging the position of class members in an inheritance hierarchy

# 10.4 Support for Refactoring

Even the simplest refactoring operation, e.g. renaming a class, method, or variable, requires careful analysis to make sure all necessary changes are made consistently.

Visual Studio and many other IDEs provide sophisticated automatic support for this activity.

Don't confuse this with a simple text editor find/replace – Visual Studio understands the C# syntax and works intelligently.. e.g. if you have local variables with the same name in two different methods and rename one of them, Visual Studio knows that if the other is a different variable and does not change it. However if you rename a public instance variable this may require changes in other classes and even in other namespaces as methods from these classes may access and use this variable.