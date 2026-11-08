of your current project and not installed somewhere. Some compilers then search for the file in the current project first.

# Don'ts for Includes

Pay attention to upper- and lowercase when naming the file, as this is observed on some systems, dear Windows users! If the header file is located in a subdirectory, always use `/` to separate it:

```
#include "MY_MODULE.H"             // ⚡ not good if the file is called "myModule.h"
#include "algo\\myModule.h"          // also use "/" under Windows
#include "c:/project/myModule.h"     // no absolute paths
#include "../algo/myModule.h"         // no relative paths with ".."
```

Instead of using the absolute path or `..`, you should store the header files somewhere else in your project and/or must adjust the search paths for header files in the compiler options. This will make it easier for you to move your project and reorganize it if necessary.

One more note on brackets versus quotation marks: Originally, `<...>` versus `"..."` meant that the header may be part of the compiler and not a file at all. However, it has become accepted that the brackets are also used if it is simply a header file that you are expected to have installed on the system. Therefore, only use `"..."` for files that are part of your project and should have priority over other libraries. Whether the priority works depends on the compiler used.

# 4.2.13  Modules

*Modules* were introduced with C++20. Instead of “copying” textual `#include` directives into a translation unit, divide your code into interface and implementation areas. To do this, use the new keywords `module` and `import`. You can find the exact usage in the C++ reference and in tutorials such as https://youtu.be/tjSuKOz5HK4 by Dos Reis. However, there is still no “best practice,” and the standard library is not yet divided into modules. With C++23, the two standard `std` and `std.compat` modules were introduced, which contain *everything* from the standard library. The `std` module contains the symbols that can be accessed with `std::`, such as `std::vector`. The `std.compat` module contains the identifiers of the global namespace, such as `::fclose`.

But today, in 2024, not much of this has been implemented with the major g++ 13, clang++ 18, and msvc++ 19.37 compilers, and some implementations are incompatible with others. As long as it is not foreseeable that modules are within reach for you, I refer you to the highly topical media if you are interested.