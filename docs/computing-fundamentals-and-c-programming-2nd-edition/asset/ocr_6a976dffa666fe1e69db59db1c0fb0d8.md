binary code. The single-pass assembler was unable to support advanced source-code optimization. As a result, the two-pass assembler was developed that read the program twice. During the first pass, all the variables and labels are read and placed into the symbol table. On the second pass, the label gaps are filled from the table by replacing the label name with the address. This helps to attain higher optimization of the source code. The translation process of an assembler consists of the following tasks:

+   - Replacing symbolic addresses like LOOP, by numeric addresses
+   - Replacing symbolic operation code by machine operation codes
+   - Reserving storage for the instructions and data
+   - Translating constants into their machine representation

# ### 2.10.2 Compiler

The compiler is a computer program that translates the source code written in a high-level language into the corresponding *object code* of the low-level language. This translation process is called *compilation*. The entire high-level program is converted into the executable machine code file. A program that translates from a low-level language to a high-level one is a decompiler. Compiled languages include COBOL, FORTRAN, C, C++, etc.

In 1952, Grace Hopper wrote the first compiler for the A-0 programming language. In 1957, John Backus at IBM introduced the first complete compiler. With the increasing complexity of computer architectures and expanding functionality supported by newer programming languages, compilers have become more and more complex. Though early compilers were written in assembly languages, nowadays it has become common practice to implement a compiler in the language it compiles. Compilers are also classified as *single-pass compilers* and *multi-pass compilers*. Though single-pass compilers are generally faster than multi-pass compilers, for sophisticated optimization, multi-pass assemblers are required to generate high-quality code.

# ### 2.10.3 Interpreter

The interpreter is a translation program that converts each high-level program statement into the corresponding machine code. This translation process is carried out just before the program statement is executed. Instead of the entire program, one statement at a time is translated and executed immediately. The commonly used interpreted language is BASIC and PERL. Although, interpreters are easier to create as compared to compilers, the compiled languages can be executed more efficiently and are faster.

# ## 2.11 PROBLEM-SOLVING TECHNIQUES

LO 2.6

In today’s world, a computer is used to solve various types of problems because it takes very less time as compared to a human being. The following steps are performed while solving a problem:

+   1. Analyse the given problem.
+   2. Divide the process used to solve the problem in a series of elementary tasks.
+   3. Formulate the algorithm to solve the problem.
+   4. Express the algorithm as a precise notation, which is known as a computer program.
+   5. Feed the computer program in the computer. CPU interprets the given program, processes the data accordingly, and generates the result.
+   6. Send the generated result to the output unit, which displays it.