Framework. Programs written using C# can use these predefined .NET classes or create their own classes.

In Example 1-1, the user-defined class is titled HelloWorld. The example also uses the Console class, one of the .NET predefined classes. Every class is named. It is traditional to name the file containing the class the same name as the class name, except the filename will have a .cs extension affixed to the end of the name. C# allows a single file to have more than one class; however, it is common practice to place one user-defined class per file for object-oriented development.

> NOTE
> Most object-oriented languages, including Java, restrict a file to one class. C#, however, allows multiple classes to be stored in a single file.

Classes are used to define controls such as buttons and labels, as well as types of things such as Student, Captain, and Employee. The word class is a keyword. Like namespaces, each class definition must be enclosed in curly braces { }. The { on Line 6 is an opening curly brace, which marks the beginning of the class definition. The opening curly brace is matched by a closing curly brace at the end of the class definition on Line 11. Within the curly braces, you define the class members. A class member is generally either a member method, which performs some behavior of the class, or a data member, which contains a value associated with the state of the class.

# Main() Method

The definition for the Main() method begins on Line 7 and ends with the closing curly brace on Line 10.

```
Line 7    static void Main( )
Line 8    {
Line 10   }
```

The Main() method plays a very important role in C#. This is the entry point for all applications. This is where the program begins execution. The Main() method can be placed anywhere inside the class definition. It begins on Line 7 for this example. When a C# program is launched, the execution starts with the first executable statement found in the Main() method and continues to the end of that method. If the application is 3000 lines long with the Main() method beginning on Line 2550, the first statement executed for the application is on Line 2550.

> NOTE
> All executable applications must contain a Main() method.