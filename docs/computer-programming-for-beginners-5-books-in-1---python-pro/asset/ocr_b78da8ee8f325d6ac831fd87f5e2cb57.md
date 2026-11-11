The code begins with the *using* statement. What this statement does is that it adds the *System* namespace into the program. C# programs normally have multiple *using statements*.

In the next line, we have a *namespace* declaration. A namespace is simply a collection of many classes. Above, we have the *HelloWorld* namespace in which we have the *Hello* class.

In the next line, we have the class declaration. The *Hello* class has method and data definitions that the program will be using. A class normally has numerous methods. The purpose of a method is to state the behavior of a class. However, our *Hello* class above only has one method, the *Main* method.

In the next line of code, we have the definition of the *Main* method, which marks the entry point for all for C# programs. It is the *Main* method that states what happens after execution of a class.

Next, we have the `/* ... */` line. This is a comment, and the C# compiler will ignore the line. The line is only meant to increase the readability of the code by human readers.

Next, we have the *Console.WriteLine(...)* line. *WriteLine* is a method that belongs to the *Console* class that is defined in the *System* namespace. This line will print the *Hello World!* message on the screen.

Lastly, we have the *Console.ReadKey();* statement. This line is for *VS.NET* users. The line will make the program to wait for a key press and prevent the screen from running then closing quickly once the program has been launched from the Visual Studio .NET.

Other than running the program from the Visual Studio, it is possible for you to run a C# program from the command prompt of the operating system. To do this, follow these sequences of steps:

+   - Open your text editor then add the code given above to it. An example of a text editor is Notepad.
+   - Save the file with the name *helloworld.cs*