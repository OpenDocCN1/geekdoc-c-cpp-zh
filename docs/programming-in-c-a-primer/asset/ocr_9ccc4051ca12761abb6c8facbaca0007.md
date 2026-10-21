# 3.12 MULTIPLE MAIN METHODS

We have stated earlier that one of the classes must have the Main method as a member. This is what is normally expected. However, C# includes a feature that enables us to define more than one class with the Main method. Since Main is the entry point for program execution, there are now more than one entry points. In fact, there should be only one. This problem can be resolved by specifying which Main is to be used to the compiler at the time of compilation as shown below:
csc filename.cs /main:classname

Program 3.11 shows a simple program that has two classes containing Main methods. We may save it in a file called multimain.cs and compile it using the switch /main:ClassA or /main:ClassB as required

```
```csharp
using System;
class ClassA
{
	public static void Main( )
	{
		Console.WriteLine("Class A");
	}
}

class ClassB
{
	public static void Main( )
	{
		Console.WriteLine("Class B");
	}
}
```
```

# 3.13 COMPILE TIME ERRORS

What we have seen so far are very simple programs. But real-life applications will contain a large number of statements with complex logic. No matter how thoroughly the design is carried out, and no matter how much care is taken in coding, we can never say that a program is totally error-free. A program may contain two types of errors:

+   - Syntax errors
+   - Logic errors

While syntax errors will be caught by the compiler. logic errors should be eliminated by testing the program logic carefully.

When the compiler cannot interpret what we are attempting to convey through our code the result is syntax error. In such situations, the compiler will detect the error(s) and display the appropriate error message(s).