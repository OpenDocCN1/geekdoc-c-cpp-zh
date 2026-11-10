# Maintenance

In this phase, developed software is made operational. Users will have lots of questions and software problems which lead to the next phase of software development. Once the software has been deployed successfully, a continuous support is provided to it for ensuring its full time availability. The software may be required to be modified if the environment undergoes a change. Maintaining and enhancing software to cope with newly discovered problems or new requirements can take far more time than the initial development of the software.

# SUMMARY

A programming language is an artificial formalism for expressing the instructions to be executed in a specified sequence. Programming languages can be classified into low-level and high level languages. Low-level programming languages include machine language and assembly language. In fact, assembly languages were so revolutionary that they became known as second-generation languages, the first generation being the machine languages themselves. Assembly languages are symbolic programming languages that use symbolic notation to represent machine-language instructions.

Most third generation languages are procedural languages. Compilers convert the program instructions from human understandable form to the machine understandable form. Interpreters also convert the source program to machine language instruction but execute each line as it is entered. The translation of the source program takes place for every run and is slower than the compiled code. The system software controls the activities of a computer, application programs, flow of data in and out of memory and disk storage. Compilation of a source code into target code follows successive stages. In lexical analysis phase, lexical units or tokens are produced from the statements. Also symbol table is constructed to record the type and attributes information of each user-defined name in the program. Next, syntax analysis takes place. In this phase, tokens are grouped into syntactic units such as expressions, and statements. That must conform to the grammatical rules of the source language to form a data structure called parse tree. In semantic analysis, the parse trees are analysed further to make sure that the operators and operands do not violate source language type specification. Then, to produce a more efficient target program, the intermediate code is generated which is then optimized. In the last phase, object code in target language is produced. Linking resolves symbolic references between object programs. A loader is a system program that accepts object programs and prepares them for execution and initiates the execution. Programming is an individual's effort and requires no formal systematic approach. Software development is more than programming. It involves a series of steps-feasibility study, requirement analysis, design, coding, testing, deployment and maintenance.

# KEY TERMS

+   * **Loader** It is a system program that accepts object programs and prepares these programs for execution by the computer and initialize the execution.
+   * **Linker** It takes one or more object files or libraries as input and combines them to produce a single (usually executable) file.
+   * **Compiler** It is a system software that translates the entire source program into machine language.
+   * **Interpreter** An interpreter is a system software that translates the source program into machine language line by line.
+   * **Syntax** It refers to the rules governing the computer operating system, the language, and the application.
+   * **Assembler** It is a program that translates an assembly language program into machine code.
+   * **Bug** It is a programming error.
+   * **Debugging** It is the process of eliminating errors from a program.
+   * **Semantic** It is the meaning of those expressions, statements, and program units.

# FREQUENTLY ASKED QUESTIONS

1. Distinguish between 3GL and 4GL.

| 3GL | 4GL |
| :--- | :--- |
| Meant for use by professional programmers. | May be used by non-professional programmers as well as by professional programmers. |
| Requires specifications of how to perform a task. | Requires specifications of what task to perform. System determines how to perform the task. |
| Requires large number of procedural instructions. | Requires fewer instructions. |
| Code may be difficult to read, understand, and maintain by the user. | Code is easy to understand and maintain. |
| Typically, file oriented. | Typically, database oriented. |

2. What are the functions of a loader?
The functions of a loader are as follows:
* Assignment of load-time storage area to the program
* Loading of program into assigned area
* Relocation of program to execute properly from its load time storage area
* Linking of programs with one another

3. What is a debugger?
The debugger is a program that lets the programmer to trace the flow of execution or examine the value of variables at various execution points in the program. For example, GDB, the GNU debugger, is used with GNU