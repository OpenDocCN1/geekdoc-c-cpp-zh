# 1.2. DEVELOPMENT TOOLS

processing is still an active area of artificial intelligence research. Natural languages, as they are used by most humans, are inherently ambiguous. To understand properly all very limited subset of natural language, a human (or artificially computer system) requires a vast amount of background knowledge that is beyond the capabilities of today's software. Fortunately, programming languages provide a relatively simple structure with strict rules for forming statements that can express a solution to any problem that can be solved by a computer.

Consider the following program fragment in the C++ programming language:

```
subtotal = 25;
tax = 3;
total = subtotal + tax;
```

These lines do not make up a C++ program; they are merely a piece of a program. The statements in this program fragment look similar to expressions in algebra. We see no sequence of binary digits. Here subtotal, tax and total variables are used to hold information. Mathematicians have used variables for hundreds of years before the first digital computer was built. In programming, a variable represents a value stored in the memory. Familiar operators (= and +) are instead of some cryptic binary digit sequence that instructs the processor to perform the operation. Since this program is expressed in the C++ language, not machine language, it cannot be executed directly on any processor. A C++ compiler is used to translate the C++ code into machine

The higher-level code is source code. The compiled machine language code is the target code. The compiler translates the source code into the target machine language.

The beauty of higher-level languages is this: the C++ source code can be compiled to different target platforms. The target platform may require changes in the source code because of architectural differences in the platforms, but the work to move from one platform to another is far less than would be necessary if the program for the new platform had to be rewritten by hand in the new language. Just importantly, when writing the program the human programmer is free to think about writing the solution to the problem in C++, not in a specific machine language.

Programmers have a variety of tools available to enhance the software development. Some common tools include:

+   - Editors. An editor allows the user to enter the program source code and save it to files. Most programming editors increase programmer productivity by using colors to highlight features. The syntax of a language refers to how we pieces of the language are arranged to make well-formed sentences. To illustrate, the sentence

The tall boy runs quickly to the door.

uses proper syntax. By comparison, the sentence

Boy the tall runs door to the is incorrect. It uses the same words as the original sentence, but their arrangement does not follow the rules of English.

Similarly, programmers must follow strict syntax rules to create well-formed computer programs. Only well-formed programs are acceptable and can be compiled and executed. Syntax aware editors can use colors or special annotations to alert programmers of syntax errors before the program is compiled.