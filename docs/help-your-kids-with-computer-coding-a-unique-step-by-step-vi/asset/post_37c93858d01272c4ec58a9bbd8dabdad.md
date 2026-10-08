
# Logic gates

Computers use electrical signals not only to understand numbers and letters but also to make decisions using devices called "logic gates". There are four main types of logic gates: "AND", "NOT", "OR", and "EXCLUSIVE OR".

# AND gate

Gates use one or more input signals to produce an output signal, based on a simple rule. AND gates switch their output signal "on" only when both input signals are "on" (1 and 1).

![](img/72d218a7a73c4d4abc7be582ebd85385_187_0.png)

Inputs 1 and 1 = output
Both input signals are "on", so the AND gate produces an "on" output signal.

Inputs 1 and 0 = output
If one input is "on" but the other is "off", the output signal is "off".

Inputs 0 and 0 = output
An AND gate produces an "off" output signal if both input signals are "off".

# NOT gate

These gates "flip" any input to its opposite. "On" input becomes "off" output, and "off" input turns to on. Gates are also known as "inverters".

> REAL WORLD
George Boole (1815–64)

George Boole was an English mathematician whose work made logic gates possible. He worked out a system to solve logic problems. This kind of math, which deals in values that can be only true or false (positive or negative), is known as "Boolean logic" in his honor.

![](img/72d218a7a73c4d4abc7be582ebd85385_187_1.png)

Input 1 = output 0
The NOT gate flips an "on" input to an "off" output, and vice versa.

# OR gate

An OR gate produces an "on" output when either one of the inputs are "on", or when both are "on".

![](img/72d218a7a73c4d4abc7be582ebd85385_188_0.png)

- Inputs 1 and 1 = output 1
Two "on" inputs produce an "on" output.

- Inputs 1 and 0 = output 1
One "on" and one "off" input still produce an "on" output.

- Inputs 0 and 0 = output 0
Only two "off" inputs produce an "off" output from an OR gate.

# EXCLUSIVE OR gate

This type of gate gives only an "on" output when one input is "on" and the other is "off". Two "on" or two "off" inputs will produce an "off" output. Gates like this are also known as "XOR" gates.

![](img/72d218a7a73c4d4abc7be582ebd85385_188_1.png)

- Inputs 1 and 1 = output 0
Two "on" inputs produce an "off" output.

- Inputs 1 and 0 = output 1
The output is only "on" when the inputs are different.

### Building computer circuits

By combining these four basic logic gates, you can create circuits to perform a whole range of advanced functions. For example, by linking an AND gate to an XOR gate, you can create a circuit that add two binary digits (bits) together. By linking two OR gates with two NOT gates in a loop, you can create a circuit that will store a bit of data (a single 1 or 0). Even the most powerful computers are based on billions of tiny logic circuits.

![](img/72d218a7a73c4d4abc7be582ebd85385_188_2.png)

Computer chips contain many logic circuits

# Processors and memory

Inside a computer are many types of electronic chips. Most importantly, the processor chip runs programs and memory chips store data for instant access.

# The processor

Processors are a collection of very small and complex circuits, printed on a glasslike material called silicon. Small switches called transistors are combined to form simple logic gates, which are further combined to form complex circuits. These circuits run all the programs on your computer.

- SEE ALSO
* 180-181 Inside a computer
* 186-187 Logic gates

![](img/72d218a7a73c4d4abc7be582ebd85385_189_0.png)

> Circuits in a processor
The circuits are kept synchronized by a clock pulse, just like an orchestra is kept in time by a conductor.

# Machine code

Processors only understand a set of program instructions called "machine code". These simple instructions for operations like adding, subtracting, and storing data are combined to create complex programs.

| 83 | 24 | f0 |
| 83 | ec | 20 |
| 44 | 24 | 1c | 00 | 00 |
| 00 | | |
| eb | 11 |
| c7 | 04 | 24 | b0 | 84 | 04 | 08 |
| e8 | id | ff | ff | ff |
| 83 | 44 | 24 | 1c | 01 |
| 7c | e8 | 24 | 1c | 09 |

Save to memory
Call another piece of code
Compare two

- Understanding machine code
Machine code is just numbers, so coders use programming languages like Python that get converted into machine code.

# Memory

Like processors, memory chips are printed on silicon. A few logic gates are combined to create a “latch circuit”. Each stores one bit (the smallest unit of data by a binary value of either 1 or 0), and many latches are combined to create megabytes and gigabytes of storage.

# RAM

Memory is often referred to as RAM ("Random Access Memory"), meaning any part of it can be accessed directly. Early types of storage could only access data in order from start to end, which was much slower.

Memory is made up of repeated identical blocks of circuit

Every item of data has a number (called an "address") so it can be found quickly

Each block of memory can store millions or billions of bits of data

# Programs and data
Programs constantly read, write, and update the data stored in the memory.

# Processing information

The processor and memory, when combined with input and output devices, give you everything you need for a computer. In a game program, for example, the user inputs data by clicking the mouse, the processor does the calculations, reads and writes memory, and then produces output in the form of making the character jump on the screen.

Contains the position of the character

A game program running

Memory click

The character jumps on screen

# Essential programs

There are a few programs that every computer needs in order to work. Some of the most important programs are operating systems, compilers, and interpreters.

# Operating system

The operating system (OS) is the manager of the computer's resources. It controls which programs are allowed to run, how long they run for, and which parts of the computer they use interfaces, such as file browsers, to let a user interact with the computer. Common operating systems include Windows and Mac OS X.

This program has run and is now waiting for its next slice of processor time

Each program has its own space in the computer's memory

![](img/72d218a7a73c4d4abc7be582ebd85385_191_0.png)

The operating system is like an octopus, with tentacles connecting to all parts of the computer

The operating system manages the processor's time

- How it works
The processor's time is divided into slices. A program will be given a slice. If it can't finish in that time, it is paused and the next program runs.

This program is waiting to run

# Compilers and interpreters

The languages you write programs with, such as Python, are known as “high-level languages”. Computer processors do not understand these languages, so compilers and interpreters are used to translate them into a low-level language (known as “machine code”) that a computer does understand.

# Compiler

![](img/72d218a7a73c4d4abc7be582ebd85385_192_0.png)

Compiler
Compilers produce translated machine code that can be saved and run later.

# Interpreter

Interpreter
Interpreters translate the code and execute the program at the same time.

![](img/72d218a7a73c4d4abc7be582ebd85385_192_1.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_192_2.png)

- Links to monitor
- Links to keyboard
- Links to speaker
- Links to mouse
- Links to printer
- Links to network

> The OS acts as a bridge between the programs you want to run and the computer’s hardware
