At the top of the file (lines 1 to 4) is a list of namespaces (see Figure 1.9). Each namespace is included by a **using directive**, which is simply the keyword using followed by the namespace. Using directives tell the compiler, and us, that we are referencing a namespace and the types declared in that namespace should be available for use.

```
1 using System;
2 using System.Collections.Generic;
3 using System.Linq;
4 using System.Text;
```

![](bbox=[0.815, 0.21, 0.935, 0.25])

Just below the using directives (see Figure 1.10), you declare a namespace named ConsoleHelloWorld (line 6) and a class named Program (line 8). Inside this class, we have defined a static function named Main (line 10). We cover classes and methods in more detail in Hour 3, but for now, think of them as a container whose boundaries are defined by the opening and closing braces.

```
6 namespace ConsoleHelloWorld
7 {
8     class Program
9     {
10        static void Main(string[] args)
11        {
12        }
13    }
14 }
```

![](bbox=[0.815, 0.42, 0.92, 0.48])

# Adding Program Statements

Now, you can focus on what we need this application to do. Because you are working in a console application, you need a way to interact with the console window that runs our application. By examining the Framework class library, you find a class named Console, which provides methods for displaying messages and receiving user input through the keyboard.

To display text in the console window, you need to enter the following statement between the braces that define Main (lines 11 and 12):

```
Console.WriteLine("Hello, world");
```

Your file should now look like Figure 1.11.

```
10        static void Main(string[] args)
11        {
12            Console.WriteLine("Hello, world");
13        }
```

![](bbox=[0.81, 0.825, 0.915, 0.88])