I include the file iostream, which is part of the standard library, because it contains code to help me display output. I surround the filename with less than (<) and greater than (>) characters to tell the compiler to find the file where it keeps all the files that came with the compiler. A file that you include in your programs like this is called a header file.

# Defining the main() Function

The next non-blank line is the header of a function called main().

```
int main()
```

A function is a group of programming code that can do some work and return a value. In this case, int indicates that the function will return an integer value. All function headers have a pair of parentheses after the function name.

All C++ programs must have a function called main(), which is the starting point of the program. The real action begins here.

The next line marks the beginning of the function.

```
{
```

And the very last line of the program marks the end of the function.

```
}
```

All functions are delimited by a pair of curly braces, and everything between them is part of the function. Code between two curly braces is called a block and is usually indented to show that it forms a unit. The block of code that makes up an entire function is called the body of the function.

# Displaying Text through the Standard Output

The first line in the body of main() displays Game Over!, followed by a newline, in the console window.

```
std::cout << "Game Over!" << std::endl;
```

"Game Over!" is a string—a series of printable characters. Technically, it’s a string literal, meaning it’s literally the characters between the quotes.

cout is an object, defined in the file iostream, that’s used to send data to the standard output stream. In most programs (including this one), the standard output stream simply means the console window on the computer screen.