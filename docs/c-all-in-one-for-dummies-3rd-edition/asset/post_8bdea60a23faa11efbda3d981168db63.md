
### Listing 6-1: Calling a Function with Only a Prototype

```cpp
#include <iostream>

using namespace std;

void BigDog(int KibblesCount);

int main()
{
    BigDog(3);
    return 0;
}
```

### Listing 6-2: Using a Function from a Separate File

```cpp
#include <iostream>

using namespace std;

void BigDog(int KibblesCount)
{
    cout << "I'm a lucky dog" << endl;
    cout << "I have " << KibblesCount << " pieces of food" << endl;
}
```

In Listings 6-1 and 6-2, we broke the function away from the prototype. When you compile these two files together as a single application (either by pressing F9 in Code::Blocks or by using the methods described in the “Multiple source files in other compilers” section, earlier in this chapter), they all fit together nicely. You can then run the application, and you see this somewhat interesting output:

```text
I'm a lucky dog
I have 3 pieces of food
```

Notice also that we had to put the same #include lines at the start of the mystuff.cpp file. That’s because mystuff.cpp uses cout, and to use cout, it needs the `#include <iostream>` line.

![](img/6ba99460b0feb3585671a4612ff5fabb_154_0.png)

## A quick overview of namespaces

The `using namespace std;` line in Listings 6-1 and 6-2 tells the compiler to use a specific namespace, std. A namespace is a grouping of classes and functions. The `std`, or standard, namespace contains a host of useful classes and functions, such as `string`. If you don’t include this declaration, you need to prefix every use of the classes or functions found in std by typing `std::<class or function>`. For example, to use a string, you need to type `std::string`. Because this is a painful way to write code, you add the `using namespace std;` line.

## Sharing with Header Files

Breaking apart source code into multiple files is easy, but soon you may run into a problem. If you have a function — say, SafeCracker() — and this function is extremely useful and is likely to be called many times from within several other source code files, you would need a prototype for SafeCracker() in every file that calls it. The prototype may look like this:

```cpp
string SafeCracker(int SafeID);
```

But instead of typing this line in every file that uses the function, we know of an easier way. (We computer people are always looking for the easier way so that we can finally retire.) Simply put this line inside its own file, called a header file, and give the filename an .h or .hpp extension. (It’s your choice which extension you use, because it really doesn’t matter; we usually just go with .h.) For example, we might save the line `string SafeCracker(int SafeID);` in a file called `safestuff.h`.

Then, instead of typing the header line at the start of each file that needs the function, you type

```cpp
#include "safestuff.h"
```

You would then have the three source code files used for the MultipleSourceFiles2 example, which we have shown in Listings 6-3, 6-4, and 6-5. The first is main.cpp, which calls the function. The second is safestuff.h, which contains the function prototype. The third is safestuff.cpp, which contains the actual code for the function whose prototype appears in the header file. Lots of files, but now the code is broken into manageable pieces. Also, make sure that you save all three of these files in the same directory.

### Listing 6-3: Including the Header File in the main File

```cpp
#include <iostream>
#include "safestuff.h"

using namespace std;

int main()
{
    cout << "Surprise, surprise!" << endl;
    cout << "The combination is (once again)" << endl;
    cout << SafeCracker(12) << endl;
    return 0;
}
```

### Listing 6-4: Containing the Function Prototype in the Header File

```cpp
using namespace std;

#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED

string SafeCracker(int SafeID);

#endif // SAFESTUFF_H_INCLUDED
```

### Listing 6-5: Containing the Actual Function Code

```cpp
#include <iostream>

using namespace std;

string SafeCracker(int SafeID)
{
    return "11-26-16";
}
```

Before you compile this application, however, we need to give you a couple of pointers. First, the compiler *does not* compile the header file into a separate `.o` or `.obj` file. With the application in Listings 6-3 through 6-5, the compiler compiles only two files: `main.cpp` and `safestuff.cpp`. Instead of compiling the header file, when the compiler reads the `main.cpp` file and reaches the `#include` line for the header file, it temporarily switches over and reads that file, pretending that it's still reading the same `main.cpp` file. As it continues, it compiles everything as if it's all part of the `main.cpp` file. And if you include this header file in other source code files, it does the same thing again for those source files.

To get this code to compile, remember the following rules:

- **Makefiles:** If you are using a compiler where you have to handle your own Makefiles, do not add a rule for compiling the header files, which usually start with `.hpp` or `.h`. Only compile the source files, which usually start with `.cpp` or `.cc`.
- **Visual C++:** Although we've said very little so far about Microsoft Visual C++ (VC++), if you use VC++, do not add header files to your project. Only add source files. VC++ will keep a list of the header files in a tree called dependencies, but you don't add them yourself.
- **Code::Blocks:** What could be easier? You just make the files, and Code::Blocks handles all the file connectivity for you — nothing to worry about. The header and source files all show in the project list, and Code::Blocks also handles the details of which ones need to be compiled.

After you follow these rules, you can go ahead and compile and run the code in Listings 6-3 through 6-5. When you run the application, you see the following output:

```text
Surprise, surprise!
The combination is (once again)
11-26-16
```

![](img/6ba99460b0feb3585671a4612ff5fabb_157_0.png)

If you have a source file containing some functions, creating a header file that contains the associated function prototypes is generally a good practice. Then you can name the header file the same as the source file, except with a different extension. We did this in Listings 6-4 and 6-5: We named the header file safestuff.h, and the source file safestuff.cpp.

![](img/6ba99460b0feb3585671a4612ff5fabb_157_1.png)

Instead of saying header file, some people prefer to say include file. We usually say header file because, to us, include is usually a verb, and it gets kind of awkward to say something like this: “We’re pretty sure that we included the include file, but if we didn’t include the correct include file, would you please include us in your meeting; and in the discussion, we will be sure to include a few questions about how to include the proper include file. Then you can include an answer to our inclusions about the inclusions of an include file.” It’s just difficult to say, you know? So we say header file.

### Adding the header only once

Code::Blocks includes several lines in the header file by default. These lines create a symbol that tells the compiler whether a header file is already included in the source file so that the compiler doesn't add it twice. Adding a header twice is an error because then you'd define the forward reference for a function twice. Here is what you see when you initially create a header file with Code::Blocks:

```cpp
#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED

#endif // SAFESTUFF_H_INCLUDED
```

When you type the header code into Code::Blocks, type it between the `#define SAFESTUFF_H_INCLUDED` and `#endif // SAFESTUFF_H_INCLUDED` lines. The section “Using the Mysterious Header Wrappers,” later in this chapter, describes these automatic entries in detail.

### Using brackets or quotes

You may have noticed something about the code in Listing 6-3. When we included the `safestuff.h` file, we did not put it inside brackets, as we did in the other `#include` lines. Instead, we put it inside quotes:

```cpp
#include "safestuff.h"
```
