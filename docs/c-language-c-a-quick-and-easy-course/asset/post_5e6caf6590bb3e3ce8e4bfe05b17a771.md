
*assembly language*, although it represented a new step related to the purely formal *lambda calculus* system, of Alonzo Church, of 1936. The purpose of Church was to develop a language that was compatible with the Turing machine (the famous “paper computer”). By the end of 1943 an air raid on Berlin destroyed those machines, but Zuse had already started the construction of the Z4. The record of its patents came to IBM’s hands in 1946, but the completion of the Z4 in Germany only has occurred in 1949.

Also in 1943 in Pennsylvania, USA, John Von Neumann and his team developed, based on ideas of Alan Turing, of whom Neumann was advisor in Princeton, the ENIAC Coding System, to the computer that he was building. In 1946, with the machine already in operation, Neumann developed with Richard Clippinger a more substantial language, the *Short Code*.

In 1952, Lieutenant Grace Murray Hopper, mathematics professor at Harvard University, presented her language *A-0* with the first compiler in the history, as a refinement of the *Short Code*, and later she created also more advanced codes such as languages *Arith-Matic* (1954) and *Flow-Matic* (1955), using human words of English. In 1952 the *Speedcoding*, of John W. Backus, also appeared, as predecessor of the *Fortran* (formula translator) language, which was conceived in 1954 and launched commercially in 1957. Since then, many high-level languages have been developed in universities and industry.

The languages closest of the machine “understanding”, written in numeric code, such as *ARC Assembly*, are called machine languages and are considered low-level languages. The faster they are in processing, the less readable they are by the human element, for giving heed to the restrictions of the machine.

### Chronology of languages

- 1936: Lambda Calculus
- 1943: Plankalkul
- 1943: ENIAC Coding System
- 1946: ENIAC Short Code
- 1947: ARC Assembly
- 1952: A-0
- 1955: Flow-Matic
- 1957: Fortran
- 1958: Algol 58, APT
- 1959: Lisp
- 1960: Algol 60, Cobol
- 1962: Snobol
- 1964: Basic, PL/I
- 1965: Algol W
- 1967: BCPL
- 1968: Algol 68, Logo
- 1969: B, APL
- 1970: Pascal
- 1971: Forth
- 1972: C, Prolog, SQL
- 1976: Modula
- 1978: Visicalc, Matlab, C Shell
- 1979: Ada
- 1980: Smalltalk
- 1981: Modula-2
- 1983: Objective-C
- 1984: dBASE III
- 1985: Clipper, Paradox
- 1987: Perl, Mathematica
- 1988: C++
- 1991: GNU E, Python, HTML, Visual Basic
- 1993: R
- 1995: Delphi, Java, PHP, Ruby, Javascript
- 1996: CSS
- 2000: C#, D
- 2001: Visual Basic .NET
- 2004: Groovy
- 2009: Go
- 2012: Julia
- 2014: Swift

### More profitable (concerning to wage):

| | |
|---|---|
| 1. Ruby | 6. Javascript |
| 2. Objective-C | 7. C |
| 3. Python | 8. R |
| 4. Java | 9. C# |
| 5. C++ | 10. Visual Basic .NET |

### Popularity of languages in 2016, by the TIOBE Index

(www.tiobe.com/index.php/tiobe_index):

| | |
|---|---|
| 1. Java | 11. Perl |
| 2. C | 12. Delphi |
| 3. C++ | 13. Visual Basic |
| 4. C# | 14. Swift |
| 5. Python | 15. Matlab |
| 6. PHP | 16. Pascal |
| 7. Visual Basic .NET | 17. Groovy |
| 8. Javascript | 18. Objective-C |
| 9. Assembly | 19. R |
| 10. Ruby | 20. PL |

Remark: In January 2015 the first place in popularity was C, which lost its position to Java, but Java and JavaScript languages are derived from C, the latter having basically the same syntax. CSS, HTML and SQL are not Turing-complete languages (Turing-complete language is one that has computational power equivalent to the Turing machine, i.e., the language and the universal Turing machine can emulate each other).

## CHAPTER 1

## THE COMPILER

The high-level languages are classified into compiled and interpreted. A program written in interpreted language is executed through the reading line by line made by the processor. Whereas a program in compiled language runs in a comprehensive manner by the processor, which then works much faster.

The first presentation written and debugged of a program on the screen is called a “source program” and in this state the program is executed if the programming code is an interpreted language. If, instead, we are working with a compiled language, so we need to pass the source program for the compiling phase, which turns it into object program and assigns it a name that usually has the .OBJ extension, as in CONTROL.OBJ. The program that performs this process is called a compiler, which exists in different versions, either for C language, C++, Clipper, Delphi, Visual Basic, or for many other codes.

The compilation phase, however, is not the final step in developing a program. The program with .OBJ extension, called object program, to become executable must go through the process of link-editing, getting an extension as .EXE, .DLL, .COM, etc.

The C language features a compiler, and not an interpreter, being therefore a language that allows the creation of very fast execution programs. A source program in C has the .CPP (C++ or C Plus Plus) or simply .C extensions.

### Structured languages

One of the elements that facilitate the work of the compiler in C is that this language favors writing structured programs, i. e., programs designed in modules that compose or mate themselves, allowing to avoid the use of deviations given by the goto statement, although such an instruction still takes part of the language.

The basic quality criterion for the development of programs is the runtime economy and memory usage of the machine. Given two versions of a program, the preferred is the one that best meets that criterion and, therefore, a program written in a structured form earns points, unless it wastes time and memory for nothing.

Once the source program is typed it should be saved to a file format, having received thus a name that should be one to eight characters, starting by letter or dash (underscore: “_”) and followed by letters, digits or numbers. Its extension should be .C to any C compiler and may be .CPP in the case of C++ compilers.

C++ compilers provide appropriate environments for programming, organized in windows and buttons, where you can enter, compile, link-edit and run the program, using for these three last steps the keyboard or only the mouse. We can reproduce program snippets in C++ environment by the technique of marking (highlighting) the text, transporting it to the clipboard - Ctrl + Ins keys - and, hence, tossing it in C++ screen - Shift + Ins keys - when then it must be unmarked - Ctrl + KH keys.

The environment of Borland Turbo C++ compiler has received the name of Integrated Development Environment (IDE) and is part of the directory named BIN. To enter this directory, type, from the DOS prompt, cd \TurboC\BIN and key to enter. Being in the directory, access to the environment is obtained by typing BC, Enter, this being just one of the ways to get to the Turbo C++ environment. Obviously, if at the time of starting (boot) the AUTOEXEC.BAT file contains the ‘Path’ the words “C:\TurboC\BIN;”, it is enough to key BC and Enter on any directory prompt, either at the root, the Windows Run or a strange directory, to immediately enter the C++ environment. To activate any of the BC Environment window just press F10 and arrows (¬, _, ®). In C++ compilers for other brands, proceed in a similar manner, adapting the words. By the way, Microsoft activates windows with Alt.

Get Borland TurboC++ 3.0 on: http://winworldpc.com (decompress with 7z and then WinImage)

### Compilation

Nothing prevents to operate, however, in the old way, by entering the .C extension program in any word processor, or in the DOS itself, and by making the compilation and link-editing right there at the operating system prompt. A program called, for example, TEST1.C, recorded in the current directory, can be compiled by typing C TEST1.C, CL TEST1.C, or TC TEST1.C, depending on whether the call to your compiler is C, CL or CT, or even another as EC, CC, BCC or LC. Borland TurboC++ 3.0 compiler uses the TCC command to work on the command line. So if TEST1.C is in the \TurboC\Progs folder, since we are in \TurboC\bin, just do TCC \TurboC\Progs\TEST1.C for the program to compile the file, and to generate in the current directory the file TEST1.EXE. Now writing on the command line the TEST1 name, it starts running.

The reader can also download the GNU compiler, GCC, the Gnu Compiler Collection, for Windows or Linux. With it, the compilation is done from the command prompt. If it is installed in Mingw folder, you should go to the Bin subdirectory, by typing CD \Mingw\bin. If your software sources are stored in \Mingw\Programs folder, and there, for example, Newtest.c program is recorded, to compile it you should type, being in the
