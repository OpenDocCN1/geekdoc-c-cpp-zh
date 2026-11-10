+   - The standard library containing the object code of all functions that are part of ANSI C (like `printf`).
+   - An editor to edit programs and header files.
+   - A debugger to locate semantic (runtime) errors in programs.

Compiling software is available in both CUI and GUI flavors. Command-line or CUI systems offer separate programs for editing, processing and debugging. These programs are invoked by name and they support several *options* or *switches* that change their default behavior. We won’t need to use these options in this book though (except in Chapter 17).

GUI-based systems offer an *Integrated Development Environment (IDE)* where all actions are invoked by the point-and-click mechanism of the mouse. IDEs are menu-based which dispenses with the need to invoke commands by name. Behind the hood, however, these mouse clicks internally invoke standalone programs. Generally, IDE systems also offer a CUI mode for those (this author included) who prefer to invoke commands by name.

# 4.3.1  GCC (Linux)

Linux systems support a CUI system called GCC, the free-to-use package from GNU. It is shipped with every Linux distribution but may not be installed by default. It comprises the following standalone programs: **gcc** (compiler), **cpp** (preprocessor), **ld** (linker) and **gdb** (debugger). GCC doesn’t offer an editor, but Linux supports two powerful editors that are used by most people: **vim** and **emacs**. To check whether GCC is installed on your system, run the **gcc** command from a shell:

```
$ gcc
gcc: no input files
```

> The $ signifies the shell prompt
> gcc exists

This message from the **gcc** compiler points out that a filename needs to be specified. If the GCC package is not installed, you’ll get the message `gcc: command not found`. **gcc** also acts as a frontend to **cpp** and **ld**, so you don’t normally have to bother about running the preprocessor and linker separately. By default **gcc** creates the executable **a.out** which has to be executed as **./a.out**.

# 4.3.2  Microsoft Visual Studio (Windows)

Unlike in Linux, C compiling software is not native to the Windows operating system. But numerous third-party packages are available including the GCC package that has also been ported to this platform. For this book, we’ll refer to the popular GUI-based Visual Studio package, where the *Build* menu in the menu bar offers all the necessary processing options. The essential programming activities and their associated menu options are listed below:

+   - Compile the program with *Build > Compile*.
+   - Invoke the linker with *Build > Build*.
+   - Execute the program with *Build > ! Execute*.

Unlike GCC, Visual Studio supports a built-in editor having limited capabilities. It also permits command-line operation from an MS-DOS shell. The commands to compile and link are **cl.exe** and **link.exe**, respectively. Like **gcc**, **cl.exe** directly invokes the linker (**link.exe**) to create the