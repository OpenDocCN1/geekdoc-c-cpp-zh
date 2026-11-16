Windows platform, and Apple Mac developers often use the XCode IDE. Appendix A provides an overview of how to use the Visual Studio 2015 IDE to develop a simple C++ program.

The myriad of features and configuration options in these powerful IDEs can be bewildering to those learning how to program. In a command-line environment the programmer needs only type a few simple commands into a console window to edit, compile, and execute programs. Some developers prefer the simplicity and flexibility of command-line build environments, especially for less complex projects.

One prominent command-line build system is the GNU Compiler Collection (http://gcc.gnu.org), or GCC for short. The GCC C++ compiler, called g++, is one of most C++ standards conforming compilers available. The GCC C++ compiler toolset is available for the Microsoft Windows, Apple Mac, and Linux platforms, and it is a free, open-source software project with a world-wide development team. Appendix B provides an overview of how to use the GCC C++ compiler.

Visual Studio and XCode offer command line development options as well. Appendix B provides an overview of the Visual Studio command line development process.

# ## 2.3 Variations of our simple program

Listing 2.2 (simple2.cpp) shows an alternative way of writing Listing 2.1 (simple.cpp).

```
```cpp
Listing 2.2: simple2.cpp

#include <iostream>

using std::cout;

int main() {
    cout << "This is a simple C++ program!\n";
}
```
```

The using directive in Listing 2.2 (simple2.cpp) allows us to use a shorter name for the std::cout printing object. We can omit the std:: prefix and use the shorter name, cout. This directive is optional, but if we omit it, we must use the longer name. The name std stands for "standard", and the std prefix indicates that cout is part of a collection of names called the standard namespace. The std namespace holds names for all the standard C++ types and functions that must be available to all standards-conforming C++ development environments. Components outside the standard library provided by third-party developers reside in their own separately-named namespaces. These include open-source projects and commercial libraries.

Listing 2.3 (simple3.cpp) shows another way to use the shorter name for cout within a C++ program.

```
```cpp
Listing 2.3: simple3.cpp

#include <iostream>

using namespace std;

int main() {
    cout << "This is a simple C++ program!\n";
}
```
```

While Listing 2.2 (simple2.cpp) made the name cout known to the compiler via its focused using directive, Listing 2.3 (simple3.cpp) provides a blanket using directive that makes all names in the std