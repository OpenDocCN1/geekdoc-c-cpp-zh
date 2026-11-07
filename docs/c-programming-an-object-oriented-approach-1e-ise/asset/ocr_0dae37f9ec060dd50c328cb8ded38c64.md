It is the job of the programmer to write the program and then to turn it into an **executable file**. There are four steps in this process:

+   a. Write and edit the program.
+   b. Compile the program.
+   c. Link the program with the required library modules (normally done automatically).
+   d. Execute the program. From our point of view, executing the program is one step.
+       From the computer point of view, however, it is two substeps: load the program and run the program.

# ### 1.5.1 Write and Edit Programs

The software used to write programs is known as a **text editor**. A text editor helps us enter, change, and store character data. Depending on the editor on our system, we could use it for writing letters, creating reports, or writing programs. The big difference between the other forms of text processing and writing programs is that programs are oriented around lines of code, while most text processing is oriented around characters and paragraphs.

The text editor could be a generalized word processor, but it is more often a special editor provided by the company that supplies the compiler. Some of the features we look for in an editor are search commands that are used to locate and replace statements, copy-and-paste commands that can be used to copy or move statements from one part of a program to another, formatting commands that use colors to display key parts of the program, and automatic formatting that aligns and indents parts of the program.

After we complete a program, we save our file to disk. This file then becomes the input to the compiler; it is known as a **source file**.

# ### 1.5.2 Compile Programs

The information in a source file stored on disk must be translated into machine language so the computer can understand it. This is the job of the **compiler**.

# ### 1.5.3 Link Programs

As we will see later in the text, a program is made up of many functions. Some of these functions are written by us and are part of our source program. However, there are other functions, such as input/output processes and mathematical library functions, that exist elsewhere and must be attached to our program. The **linker** assembles the system functions and ours into the executable file.

# ### 1.5.4 Execute Program

Once the program has been linked, it is ready for execution. To execute a program we use an operating system command, such as run, to load the program into main memory and execute it. Getting the program into memory is the function of an operating system program known as the **loader**. It locates the **executable program** and reads it into memory. When everything is ready, control is given to the program and it begins execution.

In a typical program execution, the program reads data for processing, either from the user or from a file. After the program processes the data, it prepares the output. Data output can be written to the user’s monitor or to a file. When the program is finished, it tells the operating system, which removes the program from memory.