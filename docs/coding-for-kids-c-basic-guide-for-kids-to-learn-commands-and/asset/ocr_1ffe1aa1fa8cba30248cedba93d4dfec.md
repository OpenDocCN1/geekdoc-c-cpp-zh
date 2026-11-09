```
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name;
    cout << "Enter the input string:";
    getline (std::cin, name);
    cout << "String entered: " << name << "\n";
    int size = name.size();
    cout<<"Size of string : "<<size<<endl;
}

Output:

Enter the input string: Software Testing Help
String entered: Software Testing Help!
Size of string: 21
```
```

The headers <iostream> and <string> are used here. The <iostream> library defines data types and various input/output methods. The <string> header contains string functions like getline and size.

# User-Defined Functions

Users of C++ can also define their own functions. These are the functions that the user has defined. The functions can be defined anywhere in the program and then called from anywhere in the code. Functions, like variables, must be declared before use.

Let us take a closer look at user-defined functions.

The following is the general syntax for user-defined functions (or simply functions):

```
```text
return_typefunctionName(param1,param2,...param3)
{
Function body;
}
```
```

As a result, each function, as described above, has:

The value that functions return to the caller function after completing a task is known as the return type.

+   - **functionName** : A unique identifier for naming a function.
+   - **List of parameters:** In the above syntax, these parameters are denoted by param1, param2,...paramn. When a function call is made, these are the arguments that are provided to the function. We can have functions with no parameters because the parameter list is optional.
+   - A group of statements that perform a specified purpose is referred to as a function body.

As previously stated, we must first "declare" a function before utilizing it.

# 7.3 Function Declaration and Definition

# Declaration of a Function

A function declaration informs the compiler about the function's return type, the number of parameters it uses, and