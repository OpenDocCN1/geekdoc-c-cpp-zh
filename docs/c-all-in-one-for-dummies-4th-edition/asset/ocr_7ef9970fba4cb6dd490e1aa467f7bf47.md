# # A QUICK OVERVIEW OF NAMESPACES

The `using namespace std;` line in Listing 7-2 tells the compiler to use a specific namespace, `std`. A `namespace` is a grouping of classes and functions. The `std`, or standard, namespace contains a host of useful classes and functions, such as `string`. If you don't include this declaration, you need to preface every use of the classes or functions found in `std` by typing `std::class` or `function`. For example, to use a `string`, you need to type `std::string`. Because this is a painful way to write code, you add the `using namespace std;` line.

Notice that `main.cpp` doesn't contain either `#include <iostream>` or `using namespace std;` because it doesn't have any calls to `cout`, just the call to `BigDog()`. You do have to put the `#include <iostream>` and `using namespace std;` lines at the start of the `mystuff.cpp` file because `mystuff.cpp` does use `cout`.

# ## Sharing with Header Files

Breaking apart source code into multiple files is easy, but soon you may run into a problem. If you have a function — say, `SafeCracker()` — and this function is extremely useful and is likely to be called many times from within several other source code files, you would need a prototype for `SafeCracker()` in every file that calls it. The prototype may look like this:

```
```c++
string SafeCracker(int SafeID);
```
```

But there is an easier way of adding the prototype instead of adding it to every file that uses the function. Simply put this line inside its own file, called a header file, and give the filename an `.h` or `.hpp` extension. (It's your choice which extension you use, because it really doesn't matter; most developers use `.h`.) For this example, you place the line `string SafeCracker (int SafeID);` in a file called `safestuff.h`.

Then, instead of typing the header line at the start of each file that needs the function, you type

```
```c++
#include "safestuff.h"
```
```

Splitting Up Source Code Files