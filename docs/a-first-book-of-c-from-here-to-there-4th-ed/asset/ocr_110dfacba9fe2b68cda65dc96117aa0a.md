# Program 1.1

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello there world!";

    return 0;
}
```
```

The first line of the program is a preprocessor command that uses the reserved word `include`:

`#include <iostream>`

**Preprocessor commands** begin with a pound sign (#) and perform some action before the compiler translates the source program into machine code. Specifically, the #include preprocessor command causes the contents of the named file—in this case, iostream—to be inserted wherever the #include command appears in the program. The iostream file is part of the standard library that contains, among other code, two classes: istream and ostream. These two classes provide data declarations and methods used for data input and output, respectively. The iostream file is called a **header file** because a reference to it is always placed at the top, or head, of a C++ program by using the #include command. You might be wondering what the iostream file has to do with this simple program. The answer is that the cout object is created from the ostream class. Therefore, the iostream header file must be included in all programs using cout. As shown in Program 1.1, preprocessor commands don’t end with a semicolon.

Following the preprocessor #include command is a statement containing the reserved word using. The following statement, for example, tells the compiler where to find header files in the absence of an explicit designation:

`using namespace std;`

You can think of a **namespace** as a file the compiler accesses when it’s looking for prewritten classes or functions. Because the iostream header file is contained in a file named std (for the standard library), the compiler automatically uses iostream’s cout object from this namespace whenever cout is referenced.⁷ By using namespaces, you can create your own classes and functions with the same names the standard library provides and place them in differently named namespaces. You can then tell the program which class or function to use by specifying the namespace where you want the compiler to look for the class or function.

The using statement is followed by the start of the program’s main() function, which begins with the header line described previously. The body of the function, enclosed in braces,