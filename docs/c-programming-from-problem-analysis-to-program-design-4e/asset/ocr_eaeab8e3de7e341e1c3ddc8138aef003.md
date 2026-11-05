The statement in the Main() method is a call to another method named WriteLine(). A method call is the same as a method invocation. Like Main(), WriteLine() has a signature. The heading along with the complete body of the method is the definition of the method. When called, WriteLine() writes the string argument that appears inside the parentheses to the standard output device, a monitor. After displaying the string, WriteLine() advances to the next line, as if the Enter key had been pressed.

> A quick way to identify a method is by looking for parentheses; methods always appear with parentheses (). A call to any method, such as WriteLine(), always includes a set of parentheses following the method name identifier, as do signatures for methods.

The string of text, "Hello World!", placed inside the parentheses is the method's argument. WriteLine() is defined in the Console class and can be called with no arguments. To have a blank line displayed on the standard output device, type:

```
Console.WriteLine( );   // No string argument is placed inside ()
```

The Console class contains the standard input and output methods for console applications. Methods in this class include Read(), ReadKey(), ReadLine(), Write(), and WriteLine(). The method Write() differs from WriteLine() in that it does not automatically advance the carriage return to the next line when it finishes. The following lines would produce the same result as the single line Console.WriteLine("Hello World!");

```
Console.Write("Hello");
Console.Write(" ");
Console.WriteLine("World!");
```

An invisible pointer moves across the output screen as the characters are displayed. As new characters are displayed, it moves to the next position and is ready to print at that location if another output statement is sent. Notice the second statement in the preceding code, Console.Write(" "); this places a blank character between the two words. After displaying the space, the pointer is positioned and ready to display the W in World. The output for both of the preceding segments of code is:

![](bbox=[0.22, 0.9, 0.38, 0.95])

Usually, the characters inside the double quotes are displayed exactly as they appear when used as an argument to Write() or WriteLine(). An exception occurs when an escape character is included. The backslash ( '\' ) is called the escape character. The escape character is combined with one or more characters to create a special escape sequence, such as '\n' to represent advance to next line, and '\t' for a tab indentation. A number of escape sequences can be used in C#. This is the same set of escape characters found in other languages such as Java and C++. Table 1-1 lists some of the more commonly used escape characters that can be included as part of a string in C#.