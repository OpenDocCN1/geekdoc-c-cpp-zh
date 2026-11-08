Given the scope of the language and the extent of the library, it's not unusual for a beginner to find C++ somewhat daunting. It is too extensive to learn in its entirety from a single book. However, you don't need to learn all of C++ to be able to write substantial programs. You can approach the language step-by-step, in which case it really isn't difficult. An analogy might be learning to drive a car. You can certainly become a competent and safe driver without necessarily having the expertise, knowledge, and experience to drive in the Indianapolis 500. With this book you can learn everything you need to program effectively in C++. By the time you reach the end, you'll be confidently writing your own applications. You'll also be well equipped to explore the full extent of C++ and its Standard Library.

# # C++ Program Concepts

There will be much more detail on everything we discuss in this section later in the book. We'll jump straight in with the complete, fully working C++ program shown in Figure 1-1, which also explains what the various bits are. We'll use the example as a base for discussing some more general aspects of C++.

```
```cpp
// Ex1_01.cpp
// A complete C++ program

import <iostream>;

int main()
{
    int answer {42};    // Defines answer with value 42

    std::cout << "The answer to life, the universe, and everything is "
              << answer
              << std::endl;

    return 0;
}
```
```

*Figure 1-1. A complete C++ program*

# # Source Files

The file depicted in Figure 1-1, Ex1_01.cpp, is in the code download for the book. The file extension, .cpp, indicates that this is a C++ source file or implementation file. Source files contain function bodies and thus most of the executable code in a program. The names of source files usually have the extension .cpp, although other extensions such as .cc, .cxx, or .C++ are sometimes used to identify a C++ source file.