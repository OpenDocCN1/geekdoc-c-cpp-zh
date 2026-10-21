# Chapter 6

Write a program that will call this function through a pointer and verify that it works. You’ll need an #include directive for the <cstring> header in your program to use the strlen() function.

2. Write a family of overloaded functions called equal(), which take two arguments of the same type, returning 1 if the arguments are equal, and 0 otherwise. Provide versions having char, int, double, and char* arguments. (Use the strcmp() function from the runtime library to test for equality of strings. If you don’t know how to use strcmp(), search for it in the online help. You’ll need an #include directive for the <cstring> header file in your program.) Write test code to verify that the correct versions are called.

3. At present, when the calculator hits an invalid input character, it prints an error message, but doesn’t show you where the error was in the line. Write an error routine that prints out the input string, putting a caret (^) below the offending character, like this:

```
12 + 4,2*3
  ^
```

4. Add an exponentiation operator, ^, to the calculator, fitting it in alongside * and /. What are the limitations of implementing it in this way, and how can you overcome them?

5. (Advanced) Extend the calculator so it can handle trig and other math functions, allowing you to input expressions such as:

```
2 * sin(0.6)
```

The math library functions all work in radians; provide versions of the trigonometric functions so that the user can use degrees, for example:

```
2 * sind(30)
```