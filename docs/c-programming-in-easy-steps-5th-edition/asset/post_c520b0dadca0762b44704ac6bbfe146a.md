
![](img/bf8dbdfb89042fadbaa73b4160c74bac_88_0.png)

Manipulators marked with an * are the default behaviors.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_88_1.png)

manipulate.cpp

- **1.** Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- **2.** Add a main function containing a final **return** statement and declaring two initialized variables.

```cpp
int main()
{
    bool isTrue = 1;
    int num = 255;
    // Add more statements here.
    return 0;
}
```

- **3.** In the main function, insert statements to set the width and fill of an output stream, then output a text string on it.

```cpp
cout.width(40);
cout.fill(' ');
cout << "Output" << endl;
```

- **4.** Next, insert statements to set the precision of an output stream to stop truncation of decimal places — then output a floating point number showing all its decimal places.

```cpp
cout.precision(11);
cout << "Pi: " << 3.1415926536 << endl;
```

- **5.** Now, insert statements that use manipulators to output the variable values in modified formats.

```cpp
cout << isTrue << ": " << boolalpha << isTrue << endl;
cout << num << ":" << hex << showbase << uppercase << num << endl;
```

- **6.** Save, compile, and run the program to see the output.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_88_2.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_88_3.png)

Manipulators affect all input or output on that stream. For example, the **boolalpha** manipulator will display all Boolean values on that stream in written form.

## Predicting problems

Despite the best efforts of the programmer, C++ programs may unfortunately contain one, or more, of these three types of bugs:

- **Syntax errors** – the code contains incorrect use of the C++ language. For example, an opening brace does not have a matching closing brace.
- **Logic errors** – the code is syntactically correct, but attempts to perform an operation that is illegal. For example, the program may attempt to divide a number by zero, causing an error.
- **Exception errors** – the program runs as expected until an exceptional condition is encountered that crashes the program. For example, the program may request a number, which the user enters in word form rather than in numeric form.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_89_0.png)

The C++ standards allow the compiler to spot “compile-time” errors involving syntax and logic, but the possibility of exceptional errors is more difficult to locate as they only occur at “run-time”. This means that the programmer must try to predict problems that may arise and prepare to handle those exceptional errors.

The first step is to identify which part of the program code that may, under certain conditions, cause an exception error. This can then be surrounded by a “try” block, which uses the **try** keyword and encloses the suspect code within a pair of braces.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_89_1.png)

Always consider that the user will perform the unexpected – then ensure your programs can handle those actions.

When an exception error occurs, the **try** block then “throws” the exception out to a “catch” block, which immediately follows the **try** block. This uses the **catch** keyword and encloses statements to handle the exception error within a pair of braces.

The program described below has a **try** block containing a loop that increments an integer. When the integer reaches five, a **throw()** function manually throws an exception to the **catch** block exception handler, passing the integer argument.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_89_2.png)

- **1.** Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- **2.** Add a main function containing a final **return** statement and declaring an integer variable for increment by a loop.

```cpp
int main()
{
    int number;
    // Add more statements here.
    return 0;
}
```

## Recognizing exceptions

When a program exception occurs within a **try** block, an “exception” object is automatically thrown. A reference to the exception can be passed to the associated **catch** block in the parentheses after the **catch** keyword. This specifies the argument to be an **exception** type, and a chosen exception name prefixed by the & reference operator. For example, **exception &error**.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_91_0.png)

More on references in the next chapter.

Once an exception reference is passed to a **catch** block, an error description can be retrieved by the exception's **what()** function:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_91_1.png)

- **1.** Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <string>    // Include string support.
#include <iostream>
using namespace std;
```

- **2.** Add a main function containing a final **return** statement and declaring an initialized **string** variable.

```cpp
int main()
{
    string lang = "C++";
    // Add more statements here.
    return 0;
}
```

- **3.** In the main function, insert a **try** block containing a statement attempting to erase part of the **string** variable.

```cpp
try { lang.erase(4, 6); }
```

- **4.** Next, insert a **catch** block containing a statement to send a description to standard error output by the **cerr** function.

```cpp
catch (exception &error)
{ cerr << "Exception: " << error.what() << endl; }
```

- **5.** Save, compile, and run the program to see the error description of the caught exception.

![Command Prompt screenshot](image_3)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_91_3.png)

The error description will vary for different compilers – the Visual C++ compiler describes the exception error in this example as an “invalid string position”.

The C++ **<stdexcept>** library defines a number of exception classes. Its base class is named “exception”, from which other classes are derived, categorizing common exceptions.

Each of the exception classes are listed in the table below, illustrating their relationship and describing their exception type:

| Exception class: | Description: |
|---|---|
| exception | General exception |
| ├─ bad_alloc | – failure allocating storage |
| ├─ bad_cast | – failure casting data type |
| ├─ bad_typeid | – failure referencing typeid |
| ├─ logic_error | Logic exception |
| │  ├─ domain_error | – invalid domain |
| │  ├─ invalid_argument | – invalid argument in call |
| │  ├─ length_error | – invalid length for container |
| │  └─ out_of_range | – invalid element range |
| └─ runtime_error | Runtime exception |
|    ├─ range_error | – invalid range request |
|    └─ overflow_error | – invalid arithmetic request |

![](img/bf8dbdfb89042fadbaa73b4160c74bac_92_0.png)

The `cout` function sends data to standard output, whereas the `cerr` function sends error data to standard error output. These are simply two different data streams.

When the `<stdexcept>` library is made available to a program, by adding an `#include <stdexcept>` preprocessor directive, the exception classes can be used to identify the type of exception thrown to a `catch` block.

The specific exception class name can appear, in place of the general `exception` type, within the `catch` block’s parentheses.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_92_1.png)

The example described here demonstrates the use of *standard exceptions*.

Multiple `catch` blocks can be used in succession, much like `case` statements in a `switch` block, to handle several types of exception.

Additionally, exceptions can be produced manually by the `throw` keyword. This can be used to create any of the `logic_error` and `runtime_error` exceptions in the table above. Optionally, a custom error message can be specified for manual exceptions, which can be retrieved by its `what()` function.
