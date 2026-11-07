Here’s why. First, the addition operator function creates and returns a new vector that holds the sum of the two arguments. The function creates that vector by using the default constructor, which creates vectors in the `RECT` mode. Thus, the vector being assigned to `result` is in the `RECT` mode. By default, assignment assigns each member variable individually, so `RECT` is assigned to `result.mode`. If you would prefer some other behavior, such as `result` retaining its original mode, you can override default assignment by defining an assignment operator for the class. Chapter 12 shows examples of this.

By the way, it’s a simple matter to save successive positions in a file. First, you include `<fstream>`, declare an ofstream object, and associate the object with a file:

```
```cpp
#include <fstream>
...
ofstream fout;
fout.open("thewalk.txt");
```
```

Then, in the loop that calculates the result, you insert something like this:

```
```cpp
fout << result << endl;
```
```

This invokes the friend function call `operator<<(fout, result)`, causing the `os` reference parameter to refer to `fout`, thus sending output to the file. You could also use `fout` to write other information to the file, such as the summary information currently displayed by `cout`.

# Automatic Conversions and Type Casts for Classes

The next topic on the class menu is type conversion. We’ll look into how C++ handles conversions to and from user-defined types. To set the stage, let’s first review how C++ handles conversions for its built-in types. When you make a statement that assigns a value of one standard type to a variable of another standard type, C++ automatically converts the value to the same type as the receiving variable, provided that the two types are compatible. For example, the following statements all generate numeric type conversions:

```
```cpp
long count = 8;      // int value 8 converted to type long
double time = 11;    // int value 11 converted to type double
int side = 3.33;     // double value 3.33 converted to type int
```
```

These assignments work because C++ recognizes that the diverse numeric types all represent the same basic thing—a number—and because C++ incorporates built-in rules for making the conversions. Recall from Chapter 3, “Dealing with Data,” however, that you can lose some precision in these conversions. For example, assigning `3.33` to the `int` variable `side` results in `side` getting the value 3, losing the `0.33` part.

The C++ language does not automatically convert types that are not compatible. For example, the following statement fails because the left side is a pointer type, whereas the right side is a number:

```
```cpp
int * p = 10;  // type clash
```
```