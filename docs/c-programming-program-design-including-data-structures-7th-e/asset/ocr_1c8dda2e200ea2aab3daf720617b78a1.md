+   3. After processing preprocessor directives, the next step is to verify that the program obeys the rules of the programming language—that is, the program is syntactically correct—and translate the program into the equivalent machine language. The **compiler** checks the source program for syntax errors and, if no error is found, translates the program into the equivalent machine language. The equivalent machine language program is called an **object program**.
+   
+   **Object program:** The machine language version of the high-level language program.

+   4. The programs that you write in a high-level language are developed using an integrated development environment (IDE). The IDE contains many programs that are useful in creating your program. For example, it contains the necessary code (program) to display the results of the program and several mathematical functions to make the programmer’s job somewhat easier. Therefore, if certain code is already available, you can use this code rather than writing your own code. Once the program is developed and successfully compiled, you must still bring the code for the resources used from the IDE into your program to produce a final program that the computer can execute. This prewritten code (program) resides in a place called the **library**. A program called a **linker** combines the object program with the programs from libraries.
+   
+   **Linker:** A program that combines the object program with other programs in the library and is used in the program to create the executable code.

+   5. You must next load the executable program into main memory for execution. A program called a **loader** accomplishes this task.
+   
+   **Loader:** A program that loads an executable program into main memory.

+   6. The final step is to execute the program.

Figure 1-2 shows how a typical C++ program is processed.

![](bbox=[0.199, 0.649, 0.897, 0.933])

**FIGURE 1-2** Processing a C++ program