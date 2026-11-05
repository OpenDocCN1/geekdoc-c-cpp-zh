It is not absolutely necessary to change the names of the source code file and `class`. The application can run without making that change; however, to develop good habits you should change the name. It can save you time and grief when applications involve multiple classes.

The statements in Example 1-3 appeared in Example 1-1 and are repeated here without the line numbers so that you can see the final source listing.

Visual Studio generates a couple of other unnecessary lines that can be removed. For example, three of the `using` statements (Lines 2, 3, and 4) were removed. They are not needed for most of the applications you will develop. The arguments inside the parentheses for the `Main( )` method were also removed. You will read about these lines later in this book.

# ### Example 1-3

```
    // This is traditionally the first program written.

    using System;
    namespace HelloWorldProgram
    {
        class HelloWorld
        {
            static void Main( )
            {
                Console.WriteLine("Hello World!");
            }
        }
    }
```

Do remember that C# is case sensitive, meaning the name HelloWorld is a totally different name from helloWorld, even though only one character is different. So be very careful to type the statements exactly as they are shown.

To compile the **HelloWorldProgram** project, select the **Build HelloWorldProgram** option on the **Build** menu. The name **HelloWorldProgram** follows the Build option because **HelloWorldProgram** is the name of the project. Projects that contain more than one **class** are compiled using the **Build Solution** option.

To run the application, you can click **Start Debugging** or **Start Without Debugging** on the **Debug** menu bar, as illustrated in Figure 1-21. If you attempt to execute code that has not been compiled (using **Build**), the smart IDE compiles the code first. Therefore, many developers use the shortcut of bypassing the **Build** step.