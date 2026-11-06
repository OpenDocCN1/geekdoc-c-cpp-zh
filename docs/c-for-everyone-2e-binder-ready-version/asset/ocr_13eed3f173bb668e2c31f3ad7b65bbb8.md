+   15. What does the following statement print?

```
```cpp
cout << 2 * 2 << 2;
```
```

+   16. What does the following statement print?

```
```cpp
cout << "Hello" << endl << endl << "World";
```
```

**Practice It**  Now you can try these exercises at the end of the chapter: R1.7, P1.1, P1.2.

# Common Error 1.1

# Omitting Semicolons

![](bbox=[0.133, 0.278, 0.197, 0.379])

In C++ every statement must end in a semicolon. Forgetting to type a semicolon is a common error. It confuses the compiler because the compiler uses the semicolon to find where one statement ends and the next one starts. The compiler does not use line ends or closing braces to recognize the ends of statements. For example, the compiler considers

```
```cpp
cout << "Hello, World!" << endl
return 0;
```
```

a single statement, as if you had written

```
```cpp
cout << "Hello, World!" << endl return 0;
```
```

and then it doesn't understand that statement, because it does not expect the word return in the middle of an output command. The remedy is simple. Just scan every statement for a terminating semicolon, just as you would check that every English sentence ends in a period.

# Special Topic 1.1

# Escape Sequences

![](bbox=[0.148, 0.587, 0.21, 0.668])

How can you display a string containing quotation marks, such as

```
```
Hello, "World"
```
```

You can't use

```
```cpp
cout << "Hello, "World"";
```
```

As soon as the compiler reads "Hello, ", it thinks the string is finished, and then it gets all confused about World. Compilers have a one-track mind, and if a simple analysis of the input doesn't make sense to them, they just refuse to go on, and they report an error. In contrast, a human would probably realize that the second and third quotation marks were supposed to be part of the string.

Well, how do we then display quotation marks on the screen? The designers of C++ provided an escape hatch. Mark each quotation mark with a backslash character (\), like this:

```
```cpp
cout << "Hello, \"World\"";
```
```

The sequence \" denotes a literal quote, not the end of a string. Such a sequence is called an escape sequence.

There are a few other escape sequences. If you actually want to show a backslash on the display, you use the escape sequence \\. The statement

```
```cpp
cout << "Hello\\World";
```
```

prints

```
```
Hello\World
```
```