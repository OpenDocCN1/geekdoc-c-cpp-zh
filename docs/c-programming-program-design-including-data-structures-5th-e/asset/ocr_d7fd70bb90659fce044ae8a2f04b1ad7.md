code. For example, if the source code is located in a file named `firstProg.cpp`, the name of the file containing the object code is `firstProg.obj`, and the name of the file containing the executable code is `firstProg.exe`.

The extensions as given in the preceding paragraph—that is, `.cpp`, `.obj`, and `.exe`—are system dependent. Moreover, some IDEs maintain programs in the form of projects. The name of the project and the name of the source file need not be the same. It is possible that the name of the executable file is the name of the project, with the extension `.exe`. To be certain, check your system or IDE documentation.

Because the programming instructions are placed in the function `main`, let us elaborate on this function.

The basic parts of the function `main` are the heading and the body. The first line of the function `main`, that is:

```
```cpp
int main()
```
```

is called the heading of the function `main`.

The statements enclosed between the curly braces (`{` and `}`) form the body of the function `main`. The body of the function `main` contains two types of statements:

+   - Declaration statements
+   - Executable statements

**Declaration statements** are used to declare things, such as variables.

In C++, variables or identifiers can be declared anywhere in the program, but they must be declared before they can be used.

# EXAMPLE 2-27

The following statements are examples of variable declarations:

```
```cpp
int a, b, c;
double x, y;
```
```

**Executable statements** perform calculations, manipulate data, create output, accept input, and so on.

Some executable statements that you have encountered so far are the assignment, input, and output statements.

# EXAMPLE 2-28

The following statements are examples of executable statements:

```
```cpp
a = 4;                 //assignment statement
cin >> b;              //input statement
cout << a << " " << b << endl;   //output statement
```
```