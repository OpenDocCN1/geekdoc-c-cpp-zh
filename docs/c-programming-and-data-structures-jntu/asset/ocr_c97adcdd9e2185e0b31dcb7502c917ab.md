An operating system is a program that controls the entire operation of a computer system. All input/output operations are channelled through the operating system. The operating system, which is an interface between the hardware and the user, handles the execution of user programs.

The two most popular operating systems today are UNIX (for minicomputers) and MS-DOS (for microcomputers). We shall discuss briefly the procedure to be followed in executing C programs under both these operating systems.

# UNIX System

# Creating the program

Once we load the UNIX Operating system into the memory, the computer is ready to receive the program. The program must be entered into a file. The file name can consist of letters, digits and special characters, followed by a dot and a letter c. Examples of valid file names are:

+   - hello.c
+   - program.c
+   - ebg1.c

The file is created with the help of a text editor, either ed or vi. The command for calling the editor and creating the file is

```
ed filename
```

If the file existed before, it is loaded. If it does not yet exist, the file has to be created so that it is ready to receive the new program. Any corrections in the program are done under the editor. (The name of your system’s editor may be different. Check your system manual.)

When the editing is over, the file is saved on disk. It can than be referenced any time later by its file name. The program that is entered into the file is known as the source program, since it represents the original form of the program.

# Compiling and Linking

Let us assume that the program has been created in a file named ebg1.c. Now the program is ready for compilation. The compilation command to achieve this task under UNIX is

```
cc ebg1.c
```

The source program instructions are now translated into a form that is suitable for execution by the computer. The translation is done after examining each instruction for its correctness. If everything is alright, the compilation proceeds silently and the translated program is stored on another file with the name ebg1.o. This program is known as object code.

Linking is the process of putting together other program files and functions that are required by the program. For example, if the program is using exp() function, then the object code of this function should be brought from the math library of the system and linked to the main program. Under UNIX, the linking is automatically done (if no errors are detected) when the cc command is used.

If mistakes in the syntax and semantics of the language are discovered, they are listed out and the compilation process ends right there. The errors should be corrected in the source program with the help of the editor and the compilation is done again.