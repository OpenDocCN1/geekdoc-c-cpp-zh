# 563

```
// notepad-plus.sourceforge.net (Windows) and Vim (http://www.vim.org) (Windows, Mac, and
Linux) making editing source code more convenient.
```

To see how the GNU C++ build system works, we will consider Listing 2.1 (simple.cpp) from Chapter 2.
Use an editor to create a text file containing the code for Listing 2.1 (simple.cpp), and save the file with the
name simple.cpp. In Windows, notepad++ is installed and set up properly, in the command shell you can
type

```
notepad++ simple.cpp
```

This command brings a separate window with an editor. We can type the source code for Listing 2.1
(simple.cpp) and save the file.

To create the executable program by GNU C++, back in our command-line we issue the
command

```
g++ -Wall -std=c++11 -o simple simple.cpp
```

This command has five parts:

+   * g++ -Wall -std=c++11 -o simple simple.cpp
g++ invokes the GCC C++ build process. This command runs the preprocessor, followed by the
compiler, and finally the linker to produce the executable program. Even though the preprocessor and
linker are also involved, we generally say we are "compiling the code.\n* g++ -Wall -std=c++11 -o simple simple.cpp
Wall stands for "warn" and directs the compiler to be very strict when it is compiling the source
code. It goes beyond checking that the program is well-formed C++ it also warns about code
structs that many programmers consider questionable because of nature often contains
errors. The -Wall component can be interpreted to mean "warn about as many possible problems as
m". You should compile all C++ programs with this directive it enables the compiler
to catch many common mistakes that might otherwise go unnoticed. The -Wall
directive is for all C++ programmers from novice to expert.

> The C++ standards committee is responsible for defining the C++ language.
The committee defines the language specification over time. In addition adding new
features to the language, the committee also addresses shortcomings in adding
features. As a result of the committee's newer compilers can check
toroughly the validity of C++ programs. Modern compilers do a better job
of catching common programming errors.
The -Wall directive is optional sometimes developers must work with
older C++ code. The code was originally written under more relaxed C++
language rules, but it may not be worthy to rewrite the code to bring it to
modern standards. If this older code has been proven to be reliable, it may be compiled
without the more stringent checks. All new code, however, should advantage
of the newer, better checking capabilities of the most-to-date C++ compiler;
therefore, always use -Wall on the compiler command line that you write.

![](bbox=[0.235, 0.75, 0.298, 0.796])

2014 Richard L. Halterman Draft date: January 26, 2014