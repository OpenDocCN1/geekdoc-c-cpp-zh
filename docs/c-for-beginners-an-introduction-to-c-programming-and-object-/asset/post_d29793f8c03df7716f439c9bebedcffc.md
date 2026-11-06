
## C++ FOR BEGINNERS

An Introduction to C++ Programming and Object Oriented Programming with Tutorials and Hands-On Examples

Digitized by the Internet Archive in 2022 with funding from Kahle/Austin Foundation

## C++ FOR BEGINNERS

An Introduction to C++ Programming and Object Oriented Programming with Tutorials and Hands-On Examples

## Table of Contents

- 1. Introduction ..... 1
- 2. Getting Started ..... 3
- 3. Syntax ..... 17
- 4. Data Types ..... 29
- 5. Variables and Constants ..... 33
- 6. User Interaction ..... 39
- 7. Operators ..... 45
- 8. Control Structures ..... 55
- 9. Functions ..... 73
- 10. Arrays ..... 91
- 11. Strings ..... 95
- 12. Pointers ..... 101
- 13. Introduction to Object Oriented Programming ..... 111
- 14. Constructors and Destructors ..... 121
- 15. Inheritance ..... 133
- 16. Polymorphism ..... 143
- 17. Programming Examples ..... 149
- 18. Final Words ..... 157

Over the years, there have been a lot of improvements to the initial implementation of C++. *International Organization for Standardization (ISO)* standardizes C++. The first standard *ISO/IEC 14882:1998 (C++98)* was approved in 1998. The latest standard at the time of writing this book is *ISO/IEC 14882:2017 (C++17)* which was approved in 2017. Each new standard offers new features and/or improvements to the previous ones. This book follows the widely used *ISO/IEC 14882:2011 (C++11)* standard which was approved in 2011. Unless you are a professional core C++ developer whose life revolves around developing performance critical applications in C++, you should not be worried about the ever evolving C++ standards.

With this book, you will learn the basics of C++. The concepts of procedural programming as well as object oriented programming have been covered. Having some knowledge of programming, especially knowing C programming language will help although not necessary. However, you should be comfortable with using your PC/Mac. Some experience with the usage of Terminal of Linux/Mac and Command Prompt on Windows is needed.

compiling C programs and g++ is the command line utility for compiling C++ programs.

Any text editor including Notepad can be used to write C++ programs. I recommend a text editor called *Notepad++* (https://notepad-plus-plus.org/).

### 2.1.1 GCC Installation on Windows

*MinGW* (http://www.mingw.org/) and *Cygwin* (https://sourceware.org/cygwin/) projects provide the official ports of GCC for Windows. We will be using MinGW. MinGW, a short form for "Minimalist GNU for Windows", is a minimalist development environment for Windows applications. To download MinGW, visit: https://sourceforge.net/projects/mingw/files/ and download the latest installation file. Once downloaded, execute the installation file. This file will install the MinGW Installation Manager Setup Tool and not MinGW directly.

The following window should be launched once the installation file is executed:

![](img/cda5b023e23ffd0b87fc37b1da33973d_12_0.png)

Click *Install* and you will be taken to the next window:

![](img/cda5b023e23ffd0b87fc37b1da33973d_12_1.png)

Make sure the installation directory is easily accessible, do not change any other options; click *Continue*.

The setup process will now download all the required files; this may take a few minutes. After all files are fetched, the installation window will look like this:

![](img/cda5b023e23ffd0b87fc37b1da33973d_13_0.png)

Click *Continue* and the *MinGW Installation Manager* should start. This is where you will install the *GCC* compiler.

![](img/cda5b023e23ffd0b87fc37b1da33973d_13_1.png)

Click the check box next to *mingw32-gcc-g++*, click Mark for Installation. Click *Installation -> Apply Changes* from the menu bar. The installation process of *GCC* (*g++*) compiler will now start and may take a few minutes to finish.

Open *File Explorer* (or My Computer/This PC) and go to the *MinGW installation directory* (If you did not change any options during installation, it will be `C:\MinGW`), open *bin* folder and make sure that a file called `g++ (g++.exe)` is present; if so, the installation is successful. The path to this bin folder (For example, `C:\MinGW\bin`) needs to be added to the *Path environment variable* to make g++ globally accessible. To do so, open *System Properties* (Open Control Panel, search for *Advanced System Settings* in the search box and click *View advanced system settings*). Go to the *Advanced* Tab, click *Environment Variables*. Under *System Variables*, locate the variable *Path*, click *Edit*. The following box will pop up:

### Environment Variables

![](img/cda5b023e23ffd0b87fc37b1da33973d_15_0.png)

### System Properties

Computer Name · Hardware · Advanced · System Protection · Remote

### Edit System Variable

Variable name: Path
Variable value: [blurred]

OK · Cancel

### System variables

| Variable | Value |
|---|---|
| Path |  |
| PATHEXT | .COM; .EXE; .BAT; .CMD; .VBS; .VBE; .JS; … |
| Platform | MCD |
| Platformmode | KV |

New… · Edit… · Delete

OK · Cancel

There will be some value in the *Variable value* field. Add a semicolon (;) to the end of the text if it is not present and append the complete `MinGW\bin` path (For example, `C:\MinGW\bin`) to it as shown in the screenshot above. Close all the boxes by clicking *OK* one by one.

Open *Command Prompt*, type `g++` and hit Enter. If you see an error like this – “'g++' is not recognized as an internal or external command, operable program or batch file.”, there is a problem either with the installation or with the *Path* variable. In such a case follow each and every step mentioned in this section (*Section 2.1.1*) carefully. On successful installation and proper *Path* variable settings, the `g++` command should return the following error – “g++: fatal error: no input files compilation terminated.”.

This is what the *Command Prompt* will look like if the installation is successful and the *Path* variable has been properly set up:

![](img/cda5b023e23ffd0b87fc37b1da33973d_16_0.png)

### 2.1.2 GCC/Clang Installation on Linux

Most Linux operating systems come with GCC and/or Clang built-in. To check if your Linux OS has GCC and/or Clang, open Terminal/Shell and enter `g++` and `clang++` on two separate occasions.

If GCC is present, the Terminal/Shell will look like this after entering the `g++` command:

![](img/cda5b023e23ffd0b87fc37b1da33973d_17_0.png)

If Clang is present, the Terminal/Shell will look like this after entering the `clang++` command:

![](img/cda5b023e23ffd0b87fc37b1da33973d_18_0.png)

Presence of either GCC or Clang is enough to compile and execute the programs demonstrated in this book. If both compilers are absent, you will have to install either one (I recommend GCC). Installation procedure varies from OS to OS. Here are the GCC installation procedures for most common Linux operating systems:

### For Ubuntu, Linux Mint and other Debian-based systems:

Open *Terminal/Shell* and enter the following commands one by one:

```
$>sudo apt-get update
$>sudo apt-get install gcc
```

### For Manjaro, Antergos and other Arch Linux-based systems:

Open *Terminal/Shell* and enter the following command:

## 2. Getting Started

```
g++ <source .cpp file> -o <executable output file>
eg:
g++ hello.cpp -o hello
```

To compile a C++ program using Clang, the following command is used:

```
clang++ <source .cpp file> -o <executable output
file>
eg:
clang++ hello.cpp -o hello
```

If there are no errors in the source file and the compilation happens to be successful, an executable output file will be generated as specified by the **-o** option in the compile command. The executable file on Windows will automatically have the .exe extension. If the **-o** option is not set, i.e. no output file has been mentioned, an executable file called *a.out* will be generated on Linux/Mac and *a.exe* will be generated on Windows upon successful compilation.

In order to execute the compiled program, the following commands are used:

**In Linux/Mac:**

```
./<executable output file>
eg:
./hello
```

**In Windows:**

```
<executable output file>
eg:
hello.exe
```
