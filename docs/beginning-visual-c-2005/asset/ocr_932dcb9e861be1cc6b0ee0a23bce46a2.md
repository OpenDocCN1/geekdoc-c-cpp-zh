# Chapter 2

This reads a complete line of input text that is terminated when you press the Enter key. The variable line is of type String^ and stores a reference to the string that results from executing the Console::ReadLine() function; the little hat character, ^, following the type name, String, indicates that this is a handle that references an object of type String. You'll learn more about type String and handles for String objects in Chapter 4.

A statement that reads a single character from the keyboard looks like this:

```
char ch = Console::Read();
```

With the Read() function you could read input data character by character and then analyze the characters read and convert the input to a corresponding numeric value.

The Console::ReadKey() function returns the key that was pressed as an object of type ConsoleKeyInfo, which is a value class type defined in the System namespace. Here's a statement to read a key press:

```
ConsoleKeyInfo keyPress = Console ReadKey(true);
```

The argument true to the ReadKey() function results in the key press not being displayed on the command line. An argument value of false (or omitting the argument) will cause the character corresponding the key pressed being displayed. The result of executing the function will be stored in keyPress. To identify the character corresponding to the key (or keys) pressed, you use the expression keyPress.KeyChar. Thus you could output a message relating to a key press with the following statement:

```
Console::WriteLine(L"The key press corresponds to the character: {}",
    keyPress.KeyChar);
```

The key that was pressed is identified by the expression keyPress.Key. This expression refers to a value of a C++/CLI enumeration (which you'll learn about very soon) that identifies the key that was pressed. There's more to the ConsoleKeyInfo objects that I have described. You'll meet it again later in the book.

While not having formatted input in a C++/CLI console program is a slight inconvenience while you are learning, in practice this is a minor limitation. Virtually all the real-world programs you are likely to write will receive input through components of a window, so you won't typically have the need to read data from the command line.

# Using safe_cast

The safe_cast operation is for explicit casts in the CLR environment. In most instances you can use static_cast to cast from one type to another in a C++/CLI program without problems, but because there are exceptions that will result in an error message, it is better to use safe_cast. You use safe_cast in exactly the same way as static_cast. For example:

```
double value1 = 10.5;
double value2 = 15.5;
int whole_number = safe_cast<int>(value1) + safe_cast<int>(value2);
```