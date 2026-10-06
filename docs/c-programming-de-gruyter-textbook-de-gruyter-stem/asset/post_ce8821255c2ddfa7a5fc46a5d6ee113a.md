
## 2—1 Introduction

a computer to recognize, it is too obscure for human beings to understand, let alone to remember. However, in the early years of computers software engineers could only use the machine language to write programs. At that time, there was a huge gap between natural human language and the computer programming language. It took great difficulty and long cycles for software developing, while the developed software had simple functions and unfriendly interfaces.

Before long, assembly language was developed to map the machine instructions onto some mnemonic symbols, such as ADD and SUB. The gap between the programming language and human language is somewhat reduced, while the machine language is still far from the human mind. Since machine language is pretty weak in abstraction, programmers still need to consider a great many machinery details.

Nevertheless, it is still a big progress from the machine language to assembly language. It means that it is not necessary for human beings and the computer hardware system to share a same language. Programmers can use languages that suit man's ways of thinking, while the computer hardware system only needs to recognize machine instructions. Then, how to realize the communication between the two languages? A translation tool (software) is needed. The translator for an assembly language is called an assembler, which transforms the mnemonic symbols written by programmers into machine instructions, and then the computer can recognize and execute these instructions.

### 1.1.2 High-level Language

The emergence of high-level language is a great progress in programming language. It masks the details of a machine, and raises the level of abstraction. In programs we can name variables with specific meanings and use statements that are easier to understand. Through this we can correlate the specific objects a program describes when we write the program.

Structured programming that emerged in the early 1960s further enhanced the programming level. Concepts such as structured data, structured statements, data abstraction, and procedure abstraction made programs more easily reflect the structures and logic of objects. This further reduced the gap between the programming language and natural language, while their differences remained negligible. The main problem was the separation between data and operation in a program, making it difficult to create components that could closely respond to objects in the real world.

Today there are several widely-used high-level programming languages, including Fortran, BASIC, Pascal, C, etc. The C++ programming language this book introduces is also a high-level programming language, although it has some fundamental differences from other procedure-oriented languages.

### 1.1.3 Object-oriented Language

The fundamental difference between an object-oriented language and formerly programming languages is that it is designed to describe real objects in the world and their relationships more directly.

We develop software to solve problems. The business scope a problem involves is the **problem domain**. Object-oriented programming language treats things in the real world as objects with attributes and behaviors (or services), and classifies objects with common attributes (static features) and behaviors (dynamic features) through abstraction, calling them **class**. By **using** class inheritance and polymorphism, we can easily realize reuse code, significantly shorten the development cycle, and make the software style unified. Therefore, an object-oriented programming language can make a program reflect the real problem domain, and software developers can use such normal ways of human thinking to develop software.

Object-oriented programming has experienced a long stage of development. For instance, LISP-family's object-oriented language, Simula6, Smalltalk, CLU, Ada, and Modula-2 are all programming languages that more or less use the concept of “object oriented”, among which Smalltalk is the first “true” object-oriented programming language.

However, the most widely used object-oriented (OO) programming language is C++, which is extended from C. Since C++ is compatible with C and C is already familiar to most programmers, C++ has naturally become the most widely used OO programming language.

## 1.2 Object-oriented Method

A programming language is a tool for writing programs, so the progress of a programming language reflects the progress of programming design methods. We will here first introduce the basic concepts of the object-oriented method. We believe that after reading this book, you may have a sound and complete comprehension of object-oriented method.

### 1.2.1 The Origin of Object-oriented Method

Before the emergence of object-oriented method, we had been using a procedure-oriented design method. In the early days computers were used for mathematical computations, such as computing a ballistic trajectory, people had to design a method, or procedure. Therefore, the main work for software design was to figure out a procedure to solve the problem.

Along with the rapid development of hardware systems, computers have become more powerful and widely used, not only limited to mathematic computations. Because of the increasing complexity of the programs we want to solve, the structured design method that emerged in the 1960s provided an effective way for procedure-oriented programming to solve complex problems. As a result, from the 1970s to the 1980s, programming was adopted by programmers in every field of software design. The main idea of structured programming is top-down and stepwise refinement. Its program structure is divided into several basic modules by different functionalities, and these modules form a tree structure. The relationships among the modules are kept as simple as possible. Each module consists of three basic structures – sequential structure, branch structure, and loop structure. The concrete way to realize modularization is to subroutines. Due to the use of modular decomposition, function abstraction, and top-down and stepwise refinement, structured programming can effectively decompose a complex program into several subtasks that are easier to control and handle, so as to facilitate development and maintenance.

Whatever advantages structured programming may have, it is still a kind of procedure-oriented design method, which separates data and its operations. When a data structure changes, all relevant processing procedures need modifications. Any new method for an old problem may incur extra costs, making the program hard to reuse. Besides, due to the use of GUI (Graphical User Interface), software has become easier to use while being liberated. Good software should be responsive to any user operation, rather than ask its users to follow some specific steps. For example, we are all familiar with the word processor. A good word processor should be able to be used easily and at liberty, and fixed operation orders should never appear in a software specification. Therefore, it is very difficult to use procedures to describe and implement the functions of software. If we continue to take the procedure-oriented method, both development and maintenance will

Then, what is object-oriented? First, it puts the data and its operation as an interdependent and inseparable whole, which is called an Object. It abstracts common characters from objects of the same class and groups objects into a class. Most of the data in a class can only be processed by the methods of this class. A class communicates with the outside world through a simple external interface, while objects communicate with messages. Through this way, the relationships among program modules become much simpler, and the independence of modules and data safety can be better guaranteed. Besides, inheritance and polymorphism, which will be introduced in the following chapters, may further improve code reusability and facilitate the development and maintenance of software.

There are many advantages in the object-oriented method, and yet one may wonder whether it is easy for beginners to understand and master. The answer is yes.
