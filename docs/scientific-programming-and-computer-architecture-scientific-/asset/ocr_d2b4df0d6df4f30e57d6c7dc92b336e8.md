# 2.3. Building programs using GNU Make

character \. It merits careful scrutiny. The optimization level is -xHost -03. The -xHost flag ensures that the compiler generates instructions corresponding to the highest capacity of the machine. This flag is essential for our purposes.

We do not bother with debug levels such as -g or -00. The recommended optimization in icpc is -fast. We do not use that option. It turns on -ipo and interprocedural optimization, which we do not want. Other dubious flags are also turned on by -fast.

By default the icpc may use a less precise division for IEEE double-precision numbers, according to the compiler's manual. It is unclear whether the faster division is even faster or whether the flag has any effect. The -prec-div flag (line 3) forces conformance to IEEE arithmetic. The compiler manual states that the flush-to-zero optimization is used for small numbers that almost underflow. This is another “optimization” of dubious value and uncertain meaning. It is turned off using -no-fz (line 3).

The -restrict option (line 1) enables restrict pointers, a C99 feature we find to be quite valuable in the next chapter and later.

C++ member functions may accidentally redefine a class variable, leading to runtime errors. For example, state could be a data member that keeps track of the state of the class object, and a member function, which wants to set it to 1, may say state=1 instead of state=1. The -Washadow option (line 4) tells the compiler to issue a warning when variables in an outer scope are redefined in an inner scope.

The -MD and -MP options (line 4) to the icpc compiler tell it to generate a .d file listing all dependencies of the source on header files. The way dependencies of C/C++ sources handled is discussed in section 2.3.6.

A few of our programs use the FFTW library. On line 5, the make variable FFTW is set ($FFTW). The understanding is that FFTW is defined in the shell environment before calling make. Whatever is needed to find the FFTW header files. If the installation is along standard lines, the header file will be in a standard place such as /usr/local/include/, where the compiler always looks. So the shell variable FFTW can be blank or undefined. If the header is not in a standard place, the shell variable (assuming the bash shell)^9 must be set as in

```
export FFTW_INC=<dir-with-fftw-header>
```

> ^9We always assume the shell is bash.