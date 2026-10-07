# Conditional Compilation

One of the nicest things about the import file capability is that it enables you to centralize your definitions, ensuring that all programs reference the same value. Furthermore, errors discovered in one of the values contained in the include file are corrected in only one spot, thus eliminating the need to correct every program that uses the value. Any program that referenced the incorrect value would simply have to be recompiled and would not have to be edited.

# Conditional Compilation

The Objective-C preprocessor offers a feature known as conditional compilation. Conditional compilation is often used to create one program that can be compiled to run on different systems. It is also used to switch on or off statements in the program, such as debugging statements that print the values of variables or trace the flow of execution.

# The #ifdef, #endif, #else, and #ifndef Statements

Unfortunately, a program might rely on system-dependent parameters that need to be specified differently on different devices (for example, an iPhone versus an iPad) or on a particular version of the operating system (for example, Leopard Snow Leopard).

If you have a program that had so many dependencies on the particular hardware/or software of the computer system (you should minimize as much as possible), you might end up with many values that would have to be changed to run in the other environment.

You can help reduce the problem of changing these values and incorporate into the program the these defines for each machine by using the conditional compilation capabilities of the preprocessor. A simple example, the following statements have the effect of defining #imageFile to "@barnHD.png" if the symbol IPAD has been previously defined, and to "@barn.png" otherwise:

```
#ifdef IPAD
#define imageFile "@barnHD.png"
#else
#define imageFile "@barn.png"
#endif
```

As you can see here, you are allowed to put one or more spaces after the # begins a preprocessor statement.
The #ifdef, #else, and #endif statements behave as you would expect. If the symbol specified on the #ifdef line has already been defined—through a #define statement or through the command line when the program is compiled—the compiler processes lines up to a #else, #elif, or #endif; otherwise, they are ignored.