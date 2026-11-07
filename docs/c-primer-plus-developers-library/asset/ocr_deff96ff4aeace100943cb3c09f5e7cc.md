+   - Template declarations
+   - Inline functions

It’s okay to put structure declarations in a header file because they don’t create variables; they just tell the compiler how to create a structure variable when you declare one in a source code file. Similarly, template declarations aren’t to be compiled; they are instructions to the compiler on how to generate function definitions to match function calls found in the source code. Data declared const and inline functions have special linkage properties (described shortly) that allow them to be placed in header files without causing problems.

Listings 9.1, 9.2, and 9.3 show the result of dividing Listing 7.12 into separate parts. Note that you use "coordin.h" instead of <coordin.h> when including the header file. If the filename is enclosed in angle brackets, the C++ compiler looks at the part of the host system’s file system that holds the standard header files. But if the filename is enclosed in double quotation marks, the compiler first looks at the current working directory or at the source code directory (or some such choice, depending on the compiler). If it doesn’t find the header file there, it then looks in the standard location. So you should use quotation marks, not angle brackets, when including your own header files.

Figure 9.1 outlines the steps for putting this program together on a Unix system. Note that you just give the cc compile command, and the other steps follow automatically. The g++ and gpp command-line compilers and the Borland C++ command-line compiler (bcc32.exe) also behave that way. Apple Xcode, Embarcadero C++ Builder, and Microsoft Visual C++ go through essentially the same steps, but, as outlined in Chapter 1, you initiate the process differently, using menus that let you create a project and associate source code files with it. Note that you only add source code files, not header files, to projects. That’s because the #include directive manages the header files. Also you shouldn’t use #include to include source code files because that can lead to multiple declarations.

> **Caution**
> 
> In IDEs, don’t add header files to the project list and don’t use #include to include source code files in other source code files.

Listing 9.1  **coordin.h**

```
```cpp
// coordin.h -- structure templates and function prototypes
// structure templates
#ifndef COORDIN_H_
#define COORDIN_H_

struct polar
{
    double distance;    // distance from origin
    double angle;       // direction from origin
};
```
```