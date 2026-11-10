Another class of problem oriented languages is for *symbolic language manipulation*. For example, simplifying a complex algebraic expression or getting the indefinite integral of a complex expression. MATHEMATICA is a popular language of this type.

In the Internet era, a new category of languages has emerged, the *markup languages*. Mark-up languages are not programming languages. For instance, HTML, the most widely used mark-up language, is used to specify the layout of information in Web documents. However, some programming capability has crept into some extensions to HTML and XML. Among these are the Java Server Pages, Standard Tag Library (JSTL), and eXtensible Stylesheet Language Transformations (XSLT).

# ### 4.3 COMPILING, LINKING, AND LOADING A PROGRAM

A program, written in source language, is translated by the compiler to produce a program in a *target language*. The source language is usually a high-level language. The target language may or not necessarily be machine language. In most cases, the target language is assembly language, and in which case, the target program must be translated by an *assembler* into an object program. Then the object program is *linked* with other object programs to build an executable program, which is normally saved in a specified location of the secondary memory. When it is needed to be executed, the executable file is *loaded* into main memory before its execution. The whole process is managed, coordinated and controlled by the operating system. Sometimes the target language may be a language other than machine or assembly language, in which case a translator for that language must be used to obtain an executable object program.

Conceptually, the compilation process can be divided into a number of phases, each of which is handled by different modules of a compiler, as shown in Fig. 4.3.

**Lexical analysis** In this phase, the source program is scanned for lexical units (known as *tokens*) namely, identifier, operator delimiter, etc. and classify them according to their types. A table, called *symbol table*, is constructed to record the type and attributes information of each user-defined name used in the program. This table is accessed in the other phases of compilation.

**Syntax analysis** In this phase, tokens are conflated into syntactic units such as expressions, statements, etc. that must conform to the syntax rules of the programming language.

This process is known as parsing. Syntax is similar to the grammar of a language. Syntax rules specify the way in which valid syntactic elements are combined to form the statements of the language. Syntax rules are often described using a notation known as BNF (Backus Naur Form) grammar.

![](bbox=[0.46, 0.18, 0.94, 0.452])

As a result of parsing, a data structure, known as *parse tree*, is produced.

**Semantic analysis** The *semantics* of a statement in a programming language define what will happen when that statement is executed. Semantic rules assign meanings to valid statements of the language. In the semantic analysis phase, the parsed statements are analysed further to make sure that the operators and operands do not violate source language specification.

**Intermediate code generation and optimization** To make the target program a bit smaller or faster or both, many compilers produce an intermediate form of code for optimization. In most cases, the intermediate code is generated in assembly language or in a different language at a level between assembly language and machine language.

**Code generation** This is the final phase of a standard compilation which converts every statement of the optimized intermediate code into target code using predefined target language template. The target language template depends on the machine instructions of the processor, addressing modes and number of registers, etc.

If a system library containing pre-written subroutines or functions and/or separately compiled user-defined subroutines are used in a program a final linking and loading step is needed to produce the complete machine language program in an executable form.