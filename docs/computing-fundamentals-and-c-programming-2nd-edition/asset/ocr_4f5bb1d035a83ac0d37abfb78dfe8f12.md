designed to express the logic and procedure of a problem. Although, the syntax of these programming languages is different, they use English-like commands that are easy to follow. Another major advantage of third-generation languages is that they are portable. We can put the compiler (or interpreter) on any computer and create the object code. The following program represents the source code in the C language:

```
~~~c
if( n>10)
{
    do
    {
        n++;
    }while ( n<50);
}
~~~
```

# **Problem-oriented Languages**

Problem-oriented languages are used to solve specific problems and are known as the *fourth-generation languages*. These include query Languages, Report Generators and Application Generators which have simple, English-like syntax rules. Fourth-generation languages (4 GLs) have reduced programming efforts and overall cost of software development. These languages use either a visual environment or a text environment for program development similar to that of third-generation languages. A single statement in a fourth-generation language can perform the same task as multiple lines of a third-generation language. Further, the programmer just needs to drag and drop from the toolbar, to create various items like buttons, text boxes, labels, etc. Also, the programmer can quickly create the prototype of the software application.

# **Natural languages**

Natural languages are designed to make a computer to behave like an expert and solve problems. The programmer just needs to specify the problem and the constraints for problem-solving. Natural languages such as LISP and PROLOG are mainly used to develop artificial intelligence and expert systems. These languages are widely known as *fifth generation languages*.

# ## 2.10 TRANSLATOR PROGRAMS

LO 2.5

# ### 2.10.1 Assembler

An assembler is a computer program that translates assembly language statements into machine language codes. The assembler takes each of the assembly language statements from the source code and generates a corresponding bit stream using *0s and 1s*. The output of the assembler in the form of sequence of *0s and 1s* is called *object code or machine code*. This machine code is finally executed to obtain the results.

A modern assembler translates the assembly instruction mnemonics into opcodes and resolves symbolic names for memory locations and other entities to create the object code. Several sophisticated assemblers provide additional facilities that control the assemble process, facilitate program development, and aid debugging. The modern assemblers like Sun SPARC and MIPS based on RISC architectures, optimizes instruction scheduling to attain efficient utilization of CPU. The modern assemblers generally include a macro facility and are called *macro assemblers*.

Assemblers can be classified as *single-pass assemblers* and *two-pass assemblers*. The *single-pass assembler* was the first assembler that processes the source code once to replace the mnemonics with the