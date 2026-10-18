
machine language and high-level languages like C++: Any high-level language program must be translated into machine language before the computer can understand and follow the program.

## Compilers

A program that translates a high-level language like C++ to a machine language is called a compiler. A compiler is thus a somewhat peculiar sort of program, in that its input or data is some other program, and its output is yet another program. To avoid confusion, the input program is usually called the source program or source code, and the translated version produced by the compiler is called the object program or object code. The word code is frequently used to mean a program or a part of a program, and this usage is particularly common when referring to object programs. Now, suppose you want to run a C++ program that you have written. In order to get the computer to follow your C++ instructions, proceed as follows. First, run the compiler using your C++ program as data. Notice that in this case, your C++ program is not being treated as a set of instructions. To the compiler, your C++ program is just a long string of characters. The output will be another long string of characters, which is the machine-language equivalent of your C++ program. Next, run this machine-language program on what we normally think of as the data for the C++ program. The output will be what we normally conceptualize as the output of the C++ program. The basic process is easier to visualize if you have two computers available, as diagrammed in Display 1.4. In reality, the entire process is accomplished by using one computer two times.

### Compiler

A compiler is a program that translates a high-level language program, such as a C++ program, into a machine-language program that the computer can directly understand and execute.

The complete process of translating and running a C++ program is a bit more complicated than what we show in Display 1.4. Any C++ program you write will use some operations (such as input and output routines) that have already been programmed for you. These items that are already programmed for you (like input and output routines) are already compiled and have their object code waiting to be combined with your program’s object code to produce a complete machine-language program that can be run on the computer. Another program, called a linker, combines the object code for these program pieces with the object code that the compiler produced from your

## DISPLAY 1.5 Preparing a C++ Program for Running

![](img/88b1f375f11336dbd9dac8b1675d0698_45_0.png)

## SELF-TEST EXERCISES

- 1. What are the five main components of a computer?
- 2. What would be the data for a program to add two numbers?
- 3. What would be the data for a program that assigns letter grades to students in a class?
- 4. What is the difference between a machine-language program and a high-level language program?
- 5. What is the role of a compiler?
- 6. What is a source program? What is an object program?
- 7. What is an operating system?
- 8. What purpose does the operating system serve?

![](img/88b1f375f11336dbd9dac8b1675d0698_47_0.png)

![](img/88b1f375f11336dbd9dac8b1675d0698_47_1.png)

![](img/88b1f375f11336dbd9dac8b1675d0698_47_2.png)

directions, procedure, and routine. The instructions may be expressed in a programming language or a human language. Our algorithms will be expressed in English and in the programming language C++. A computer program is simply an algorithm expressed in a language that a computer can understand. Thus, the term algorithm is more general than the term program. However, when we say that a sequence of instructions is an algorithm, we usually mean that the instructions are expressed in English, since if they were expressed in a programming language we would use the more specific term program. An example may help to clarify the concept.

Display 1.6 contains an algorithm expressed in English. The algorithm determines the number of times a specified name occurs on a list of names. If the list contains the winners of each last season’s football games and the name is that of your favorite team, then the algorithm determines how many games your team won. The algorithm is short and simple but is otherwise very typical of the algorithms with which we will be dealing.

## DISPLAY 1.6 An Algorithm

Algorithm that determines how many times a name occurs in a list of names:

- 1. Get the list of names.
- 2. Get the name being checked.
- 3. Set a counter to zero.
- 4. Do the following for each name on the list:
  Compare the name on the list to the name being checked, and if the names are the same, then add one to the counter.
- 5. Announce that the answer is the number indicated by the counter.

The instructions numbered 1 through 5 in our sample algorithm are meant to be carried out in the order they are listed. Unless otherwise specified, we will always assume that the instructions of an algorithm are carried out in the order in which they are given (written down). Most interesting algorithms do, however, specify some change of order, usually a repeating of some instruction again and again such as in instruction 4 of our sample algorithm.

The word algorithm has a long history. It derives from the name al-Khowarizmi, a ninth-century Persian mathematician and astronomer. He wrote a famous textbook on the manipulation of numbers and equations. The book was entitled Kitab al-jabr w’almuqabala, which can be translated as Rules for Reuniting and Reducing. The similar-sounding word algebra was derived from the Arabic word al-jabr, which appears in the title of the book and which is often translated as reuniting or restoring. The meanings of the words algebra and algorithm used to be much more intimately related than they are today. Indeed, until modern times, the word algorithm usually referred only to algebraic rules for solving numerical equations. Today, the word algorithm can be applied to a wide variety of kinds of instructions for manipulating symbolic as well as numeric data. The properties that qualify a set of instructions as an algorithm now are determined by the nature of the instructions rather than by the things manipulated by the instructions. To qualify as an algorithm, a set of instructions must completely and unambiguously specify the steps to be taken and the order in which they are taken. The person or machine carrying out the algorithm does exactly what the algorithm says, neither more nor less.

### Algorithm

An algorithm is a sequence of precise instructions that leads to a solution.

## DISPLAY 1.7 Program Design Process

![](img/88b1f375f11336dbd9dac8b1675d0698_50_0.png)

large algorithms this will require a pencil and paper. The C++ program is tested by compiling it and running it on some sample input data. The compiler will give error messages for certain kinds of errors. To find other types of errors, you must somehow check to see whether the output is correct.

The process diagrammed in Display 1.7 is an idealized picture of the program design process. It is the basic picture you should have in mind, but reality is sometimes more complicated. In reality, mistakes and deficiencies are discovered at unexpected times, and you may have to back up and redo an earlier step. For example, as shown in Display 1.7, testing the algorithm might reveal that the definition of the problem was incomplete. In such a case you must back up and reformulate the definition. Occasionally, deficiencies in the definition or algorithm may not be observed until a program is tested. In that case you must back up and modify the problem definition or algorithm and all that follows them in the design process.

## Object-Oriented Programming

The program design process that we outlined in the previous section represents a program as an algorithm (set of instructions) for manipulating some data. That is a correct view, but not always the most productive view. Modern programs are usually designed using a method known as object-oriented programming, or OOP. In OOP, a program is viewed as a collection of interacting
