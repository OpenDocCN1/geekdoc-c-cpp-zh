make nmake to build the project. We can also use qmake to generate a Visual Studio project (.dsp .vproj) by file typing qmake -tp vc hello.pro

On Mac OS X, we can generate an Xcode project file using qmake -spec macx-xcode hello.pro

and makefiles qmake -spec macx-g++ hello.pro

The -spec command-line option lets us specify a platform/compiler combination. qmake detects the correct format, but in some cases it may be necessary to specify it explicitly. For example, to generate a makefile that invokes the Intel C++ Compiler (ICC) for Linux in 64-bit mode, we would type qmake -spec linux-icc-64 hello.pro

The possible specifications are located in Qt's mkspecs directory.

Although qmake's primary purpose is to generate makefiles from .pro files, we can also use qmake to generate a .pro file for the current directory, using the -project option: For example:

```
qmake -project
```

In this mode, qmake will search the current directory for files with known extensions (.h, .cpp, .ui, etc.) and produce a .pro file that lists these files.

In the rest of this section, we will look in more detail at the .pro file syntax. A .pro variable entry normally has the syntax variable = values

where values is a list of string values. Comments start with the pound sign (#) and terminate at the end of the line. For example, the line