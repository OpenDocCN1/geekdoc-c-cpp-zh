
![](img/d61019b035dd82beb581604273c0ee6b_30_0.png)

## Programming Tips

- Library Functions for Sorting and Binary Search 412
- Use Reference Parameters To Avoid Copies 441
- Use the auto Type for Iterators 503

![](img/d61019b035dd82beb581604273c0ee6b_30_1.png)

## Special Topics

- Oh, Omega, and Theta 399
- Insertion Sort 400
- The Quicksort Algorithm 407
- Defining an Ordering for Sorting Objects 413
- Overloading Increment and Decrement Operators 427
- Implicit Type Conversions 428
- Returning References 429
- Virtual Destructors 443
- Suppressing Automatic Generation of Memory Management Functions 443
- Move Operations 444
- Shared Pointers 445
- Non-Type Template Parameters 450
- Reverse Polish Notation 492
- Multisets and Multimaps 503
- Implementing Hash Functions 514
- Open Addressing 516

![](img/d61019b035dd82beb581604273c0ee6b_30_2.png)

## Computing & Society

- The Limits of Computation 390
- The First Programmer 418

## CHAPTER 1 INTRODUCTION

### CHAPTER GOALS

- To learn about the architecture of computers
- To learn about machine languages and higher-level programming languages
- To become familiar with your compiler
- To compile and run your first C++ program
- To recognize compile-time and run-time errors
- To describe an algorithm with pseudocode
- To understand the activity of programming

![](img/d61019b035dd82beb581604273c0ee6b_32_0.png)

© JanPietruszka/Stockphoto.

### CHAPTER CONTENTS

- 1.1 WHAT IS PROGRAMMING? 2
- 1.2 THE ANATOMY OF A COMPUTER 3
  - C&S Computers Are Everywhere 5
- 1.3 MACHINE CODE AND PROGRAMMING LANGUAGES 5
  - C&S Standards Organizations 7
- 1.4 BECOMING FAMILIAR WITH YOUR PROGRAMMING ENVIRONMENT 7
  - PT1 Backup Copies 10
- 1.5 ANALYZING YOUR FIRST PROGRAM 11
  - SYN C++ Program 12
  - SYN Output Statement 13
  - CE1 Omitting Semicolons 13
  - ST1 Escape Sequences 13
- 1.6 ERRORS 14
  - CE2 Misspelling Words 15
- 1.7 PROBLEM SOLVING: ALGORITHM DESIGN 16
  - HT1 Describing an Algorithm with Pseudocode 19
  - WE1 Writing an Algorithm for Tiling a Floor 21

![](img/d61019b035dd82beb581604273c0ee6b_33_0.png)

Just as you gather tools, study a project, and make a plan for tackling it, in this chapter you will gather up the basics you need to start learning to program. After a brief introduction to computer hardware, software, and programming in general, you will learn how to write and run your first C++ program. You will also learn how to diagnose and fix programming errors, and how to use pseudocode to describe an algorithm—a step-by-step description of how to solve a problem—as you plan your programs.

### 1.1 What Is Programming?

Computers execute very basic instructions in rapid succession.

You have probably used a computer for work or fun. Many people use computers for everyday tasks such as electronic banking or writing a term paper. Computers are good for such tasks. They can handle repetitive chores, such as totaling up numbers or placing words on a page, without getting bored or exhausted.

A computer program is a sequence of instructions and decisions.

The flexibility of a computer is quite an amazing phenomenon. The same machine can balance your checkbook, print your term paper, and play a game. In contrast, other machines carry out a much narrower range of tasks; a car drives and a toaster toasts. Computers can carry out a wide range of tasks because they execute different programs, each of which directs the computer to work on a specific task.

The computer itself is a machine that stores data (numbers, words, pictures), interacts with devices (the monitor, the sound system, the printer), and executes programs. A computer program tells a computer, in minute detail, the sequence of steps that are needed to fulfill a task. The physical computer and peripheral devices are collectively called the hardware. The programs the computer executes are called the software.

Today’s computer programs are so sophisticated that it is hard to believe that they are composed of extremely primitive operations. A typical operation may be one of the following:

- Put a red dot at this screen position.
- Add up these two numbers.
- If this value is negative, continue the program at a certain instruction.

The computer user has the illusion of smooth interaction because a program contains a huge number of such operations, and because the computer can execute them at great speed.

The act of designing and implementing computer programs is called programming. In this book, you will learn how to program a computer—that is, how to direct the computer to execute tasks.

Programming is the act of designing and implementing computer programs.

To write a computer game with motion and sound effects or a word processor that supports fancy fonts and pictures is a complex task that requires a team of many highly skilled programmers. Your first programming efforts will be more mundane. The concepts and skills you learn in this book form an important foundation, and you should not be disappointed if your first programs do not rival the sophisticated software that is familiar to you. Actually, you will find that there is an immense thrill even in simple programming tasks. It is an amazing experience to see the computer precisely and quickly carry out a task that would take you hours of drudgery, to make small changes in a program that lead to immediate improvements, and to see the computer become an extension of your mental powers.

### 1.2 The Anatomy of a Computer

To understand the programming process, you need to have a rudimentary understanding of the building blocks that make up a computer. We will look at a personal computer. Larger computers have faster, larger, or more powerful components, but they have fundamentally the same design.

At the heart of the computer lies the central processing unit (CPU) (see Figure 1). It consists of a single chip, or a small number of chips. A computer chip (integrated circuit) is a component with a plastic or metal housing, metal connectors, and inside wiring made principally from silicon. For a CPU chip, the inside wiring is enormously complicated. For example, the Pentium chip (a popular CPU for personal computers at the time of this writing) is composed of several million structural elements, called transistors.

The central processing unit (CPU) performs program control and data processing.

The CPU performs program control and data processing. That is, the CPU locates and executes the program instructions; it carries out arithmetic operations such as addition, subtraction, multiplication, and division; it fetches data from external memory or devices and stores data back.

Storage devices include memory and secondary storage.

There are two kinds of storage. Primary storage, or memory, is made from electronic circuits that can store data, provided they are supplied with electric power. Secondary storage, usually a hard disk (see Figure 2) or a solid-state drive, provides slower and less expensive storage that persists without electricity. A hard disk consists of rotating platters, which are coated with a magnetic material. A solid-state drive uses electronic components that can retain information without power, and without moving parts.

![](img/d61019b035dd82beb581604273c0ee6b_34_0.png)

![](img/d61019b035dd82beb581604273c0ee6b_34_1.png)

Programs and data are typically stored on the hard disk and loaded into memory when the program starts. The program then updates the data in memory and writes the modified data back to the hard disk.

To interact with a human user, a computer requires peripheral devices. The computer transmits information (called output) to the user through a display screen, speakers, and printers. The user can enter information (called input) by using a keyboard or a pointing device such as a mouse.

Some computers are self-contained units, whereas others are interconnected through networks. Through the network cabling, the computer can read data and programs from central storage locations or send data to other computers. For the user of a networked computer it may not even be obvious which data reside on the computer itself and which are transmitted through the network.

Figure 3 gives a schematic overview of the architecture of a personal computer. Program instructions and data (such as text, numbers, audio, or video) reside in secondary storage or elsewhere on the network. When a program is started, its instructions are brought into memory, where the CPU can read them. The CPU reads and executes one instruction at a time. As directed by these instructions, the CPU reads data, modifies it, and writes it back to memory or secondary storage. Some program instructions will cause the CPU to place dots on the display screen or printer or to vibrate the speaker. As these actions happen many times over and at great speed, the human user will perceive images and sound. Some program instructions read user input from the keyboard, mouse, touch sensor, or microphone. The program analyzes the nature of these inputs and then executes the next appropriate instruction.

![](img/d61019b035dd82beb581604273c0ee6b_35_0.png)
