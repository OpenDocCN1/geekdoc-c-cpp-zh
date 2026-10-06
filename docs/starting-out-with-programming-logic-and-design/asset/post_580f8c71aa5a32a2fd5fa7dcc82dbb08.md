
## 1.4 How a Program Works 15

> NOTE: There are many different versions of assembly language. It was mentioned earlier that each brand of CPU has its own machine instruction set. Each brand of CPU typically has its own assembly language as well.

Assembly programs cannot be executed by the CPU, however. The CPU only understands machine language, so a special program as an assembler is used to translate an assembly language program to a machine language. This process is shown in Figure 1-17. The machine language program that is created by the assembler can then be executed by the CPU.

## Figure 1-17 An assembler translates an assembly language program to a language program

![](img/c939132f78787c7f339c6977b3fc8c85_39_0.png)

## High-Level Languages

Although assembly language makes it unnecessary to write binary machine language instructions, it is not without difficulties. Assembly language is primarily a direct substitute for machine language, and like machine language, it requires that you know a lot about CPU. Because assembly language is so close in nature to machine language, it is referred as as a low-level language.

In the 1950s, a new generation of programming languages known as high-level languages began to appear. A high-level language allows you to create powerful and complex programs without knowing low-level instructions. In addition, most high-level languages use words that are easy to understand. For example, if a programmer used COBOL (which was one of the early high-level languages created in the 1950s), he or she would write the following instruction to display "Hello world" on the computer screen:

```
Display "Hello world"
```

Doing the same in assembly language would require several instructions, and an intimate knowledge of how the CPU interacts with the video card. As, high-level languages allow programmers to concentrate on the tasks they want to perform with their programs rather than the details of how the CPU will execute those programs.

Since the 1950s, thousands of high-level languages have been created. Table 1-1 lists several of the well-known languages. If you are working towards a degree in computer science or a related field, you are likely to study one or more of these languages.

## Chapter 1 Introduction to Computers and Programming

## Table 1-1 Programming languages

| Language | Description |
| :--- | :--- |
| Ada | Ada was created in the 1970s, primarily for applications used by the U.S. Department of Defense. The language is named in honor of Countess Ada Lovelace, an influential and historical figure in the field of computing. |
| BASIC | All-purpose Symbolic Instruction Code is a general-purpose language that was originally designed in the early 1960s to be simple enough for beginners to learn. Today, there are many different versions of BASIC. |
| FORTRAN | FORMLTranator was the first high-level programming language. It was designed in the 1950s for performing mathematical calculations. |
| COBOL | Common Business-Oriented Language was created in the 1950s, and was designed for business applications. |
| Pascal | Pascal was created in 1970, and was originally named in honor of the mathematical, physicist, and philosopher Pascal. |
| C and C++ | C and C++ (pronounced "c plus") are powerful, general-purpose languages developed at Bell Laboratories. The C language was created in 1972 and the C++ language was created in 1983. |
| C# | Pronounced "sharp." This was created by Microsoft around the year 2000 for developing applications based on the Microsoft .NET framework |
| Java | Java was created by Sun Microsystems (a company that is now owned by Oracle) in the early 1990s. It can be used to develop programs that run on a single computer or over the Internet from a Web server. |
| JavaScript | JavaScript, created in the 1990s, can be used in Web pages. Despite its name, JavaScript is not related to Java. |
| Python | Python is a general-purpose language created in the early 1990s. It has become popular in business and academic circles. |
| Ruby | Ruby is a general-purpose language that was created in the 1990s. It is increasingly becoming a popular language for programs that run on Web servers. |
| Visual Basic | Visual Basic (commonly known as VB) is a Microsoft programming language and software development environment that allows programmers to create Windows-based applications. Quickly, VB was originally created in the early 1990s. |

Each high-level language has its own set of words that the programmer must learn in order to use the language. The words that make up a high-level programming language are known as key words or reserved words. Each key word has a specific meaning, and cannot be used for any other purpose. You previously saw an example of a COBOL statement that the key word display to print a message on the screen. In the Python language the word print serves the same purpose.

In addition to key words, programming languages have operators that perform various operations on data. For example, all programming languages have math operators that perform arithmetic. In Java, as well as most other languages, the + sign is an operator adds two numbers. The following adds 12 and 75:

12 + 75

## 1.4 How a Program Works

In addition to key words and operators, each language has its own syntax, which is a set of rules that must be strictly followed when writing a program. The syntax rules dictate how key words, operators, and various punctuation characters must be used in a program. When you are learning a programming language, you must learn the syntax for that particular language.

The individual instructions that you use to write a program in a high-level programming language are called statements. A programming statement can consist of key words, operators, punctuation, and other allowable programming elements, arranged in the proper sequence to perform an operation.

> NOTE: Human languages also have syntax rules. Do you remember when you took your first English class, and you learned all rules about infinitives, indirect objects, classes, and so forth? You were learning the syntax of the English language.

Although people commonly violate the rules of their native language when speaking and writing, other people usually understand what they mean. Unfortunately, computers do not have this ability. If even a single syntax error appears in a program, the program cannot be executed.

## Compilers and Interpreters

Because the CPU understands only machine language instructions, programs that are written in a high-level language must be translated into machine language. Once a program has been written in a high-level language, the programmer will use a compiler or an interpreter to make the translation.

A compiler is a program that translates a high-level language program into a machine language. The machine language program that is created by the assembler can then be executed by the CPU.

## Figure 1-17 An assembler translates an assembly language program to a language program

![](img/c939132f78787c7f339c6977b3fc8c85_39_0.png)

| High-level language | Machine language |
| :--- | :--- |
| Display "Hello world" | (machine code) |

## Compilers and Interpreters

An interpreter is a program that translates and executes the instructions in a high language. As the interpreter reads each individual instruction in the program, it converts it to a machine language instruction and then executes it. This is illustrated in Figure 1-19.

## Figure 1-19 Executing a high-level program with an interpreter

![](img/c939132f78787c7f339c6977b3fc8c85_42_0.png)

| High-level language | Machine language |
| :--- | :--- |
| Display "Hello world" | (machine code) |
