```
} fclose(inFilePtr); // close the input file

else { // input file could not be opened
    printf("File \"%s\" could not be opened\n", argv[1]);
}
}
```

Fig. 14.3 | Using command-line arguments. (Part 2 of 2.)

# 14.5 Compiling Multiple-Source-File Programs

It's possible to build programs that consist of multiple source files. There are several considerations when creating programs in multiple files. For example, the definition of a function must be entirely contained in one file—it cannot span two or more files.

# 14.5.1 extern Declarations for Global Variables in Other Files

In Chapter 5, we introduced the concepts of storage class and scope. We learned that variables declared outside any function definition are referred to as global variables. Global variables are accessible to any function defined in the same file after the variable is declared. Global variables also are accessible to functions in other files. However, the global variables must be declared in each file in which they're used. For example, to refer to global integer variable flag in another file, you can use the declaration

```
extern int flag;
```

This declaration uses the storage-class specifier extern to indicate that variable flag is defined either later in the same file or in a different file. The compiler informs the linker that unresolved references to variable flag appear in the file. If the linker finds a proper global definition, the linker resolves the references by indicating where flag is located. If the linker cannot locate a definition of flag, it issues an error message and does not produce an executable file. Any identifier that's declared at file scope is extern by default.

> **Software Engineering Observation 14.1**
> 
> > Global variables should be avoided unless application performance is critical because they violate the principle of least privilege.

# 14.5.2 Function Prototypes

Just as extern declarations can be used to declare global variables to other program files, function prototypes can extend the scope of a function beyond the file in which it's defined (the extern specifier is not required in a function prototype. Simply include the function prototype in each file in which the function is invoked and compile the files together (see Section 13.2). Function prototypes indicate to the compiler that the specified function is defined either later in the same file or in a different file. Again, the compiler does not attempt to resolve references to such a function—that task is left to the linker. If the linker cannot locate a proper function definition, the linker issues an error message.