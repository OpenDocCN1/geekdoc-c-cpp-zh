object code is built using your tool chain’s native make tool, which, in turn, calls the compiler and linker. For pdCalc, on a Linux system, you’ll usemake, which will, in turn, use gcc for compiling and linking. On a Windows system, you’ll usemingw32-make, which will, in turn, use the mingw compiler and linker.

Now that you understand how qmake works, let’s examine how to build pdCalc using either Qt Creator or the command line.

# A.3.1 Using Qt Creator

If your preference is to use Qt Creator, most of the complexity of using qmake will be hidden from you. To begin, simply launch the IDE, and open the pdCalc.pro project. This file is located at the top level of the source tree.

The first time you open a qmake project file with Qt Creator, you will be presented with a configuration list asking you which version of