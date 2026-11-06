![](bbox=[0.109, 0.092, 0.259, 0.183])

+   16. What is the value of n after these statements?
+   ```cpp
+   istream strm;
+   strm.str("123,456");
+   int n;
+   int m;
+   char ch;
+   strm >> n >> ch >> m;
+   n = 1000 * n + m;
+   ```
+   17. What does `string_to_int("123,456")` return?
+   18. What does `string_to_int("$123")` return?
+   19. What is the value of `strm.str()` after these statements?
+   ```cpp
+   ostringstream strm;
+   strm << setprecision(5) << 10.0 / 3;
+   ```
+   20. Write a function that converts a floating-point number to a string. Provide a parameter variable for the number of digits after the decimal point.

**Practice It**  Now you can try these exercises at the end of the chapter: R8.9, P8.10, P8.13.

# 8.5 Command Line Arguments

Depending on the operating system and C++ development environment used, there are different methods of starting a program—for example, by selecting “Run” in the compilation environment, by clicking on an icon, or by typing the name of the program at a prompt in a command shell window. The latter method is called “invoking the program from the command line”. When you use this method, you must type the name of the program, of course, but you can also type in additional information that the program can use. These additional strings are called **command line arguments**. For example, if you start a program with the command line

```
```text
prog -v input.dat
```
```

then the program receives two command line arguments: the strings "-v" and "input.dat". It is entirely up to the program what to do with these strings. It is customary to interpret strings starting with a hyphen (-) as options and other strings as file names.

To receive command line arguments, you need to define the main function in a different way. You define two parameter variables: an integer and an array of string literals of type char*.

```
```cpp
int main(int argc, char* argv[])
{
    ...
}
```
```

Here argc is the count of arguments, and argv contains the values of the arguments. In our example, argc is 3, and argv contains the three strings

```
```text
argv[0]:  "prog"
argv[1]:  "-v"
argv[2]:  "input.dat"
```
```

Note that argv[0] is always the name of the program and that argc is always at least 1.

> Programs that start from the command line can receive the name of the program and the command line arguments in the main function.