These methods can be invoked using either Console.In object or Console class itself. The following code snippet reads a character from the keyboard and displays it on the screen.
int x = Console.Read( );
Console.WriteLine( (char) x );
We have used a casting operator ( char ) to x to convert it to a character type. Remember, x was read as an int.

The following code reads entire line of text as a single string and displays it on the screen.
string str = Console.ReadLine( );
Console.WriteLine(str);

Program 17.1 illustrates the use of ReadLine( ) method to read interactively strings from the keyboard and to echo them to the screen.

# Program 17.1 USING READLINE ( ) TO READ STRINGS

```
using System;
class ReadString
{

public static void Main ( )
{

Console.WriteLine("What is your name?");
string s;
s = Console.ReadLine ( );
Console.WriteLine("How are you Mr." + s);
}
}
```

# 17.4 CONSOLE OUTPUT

The console output stream supports two methods for writing to the console:

+   - Write ( ) Outputs one or more values to the screen without a newline character
+   - WriteLine ( ) Outputs one or more values to the screen (same as Write ( ) method) but adds a newline character at the end of the output

Both the methods have various overloaded forms for handling all the predefined types and therefore we can easily output many different types of data. WriteLine( ) also allows us to output data in many different formats (in a way, comparable to the printf method of C).

The Write( ) method sends information into a buffer. This buffer is not flushed until a newline (or end-of-line) character is sent. As a result, this method prints output on one line until a newline character is encountered. For example, the statements,
Console.Write("Hello ");
Console.Write("C Sharp!");
will display the words Hello C Sharp! on one line and wait for displaying of further information on the same line. We may force the display to be brought to the next line by printing a newline character as shown below:
Console.Write("\n");