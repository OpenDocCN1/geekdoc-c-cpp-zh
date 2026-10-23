
In the end, one of the major goals of this text is to be a book that CS students find worthy of keeping on their bookcases after they are done with the course. This is a challenging task for a CS1 and CS2 text. It is a significant part of the reason that this book, especially in the second half, includes a number of more advanced topics. It is quite possible that you will choose to not cover several of the later chapters in this book, however, they are important concepts from computing that can be difficult to find in a single source. The hope is that those topics, combined with clear and concise code solutions to many problems, will make this a book that is worth space on a bookshelf.

## Part I
### Introductory Concepts

## Chapter 1
### Basics of Computers, Computing, and Programming

- 1.1 History ......................................................... 3
- 1.2 Hardware ......................................................... 5
- 1.3 Software ......................................................... 7
- 1.4 Nature of Programming ............................................ 9
- 1.5 Programming Paradigms ........................................... 11
- 1.5.1 Imperative Programming ....................................... 11
- 1.5.2 Functional Programming ....................................... 11
- 1.5.3 Object-Oriented Programming .................................. 12
- 1.5.4 Logic Programming ............................................ 13
- 1.5.5 Nature of Scala .............................................. 13
- 1.6 End of Chapter Material ......................................... 13
- 1.6.1 Summary of Concepts .......................................... 13
- 1.6.2 Exercises .................................................... 14
- 1.6.3 Projects ..................................................... 14

In all things it is good to understand some foundational material before going into detail. This helps to ground you and give you some context. Inevitably, you already have some experience with computers and that does give you a bit of context to work in. However, it is quite possible that your experience is limited to rather recent technology. One of the factors that shapes the world of Computer Science is that it is fast moving and ever changing. Knowing how we got to where we are can perhaps help us see where we will be going.

### 1.1 History

One might think that Computer Science is a field with a rather short history. After all, computers have not existed all that long and have been a standard fixture for even less time. However, the history of Computer Science has deep roots in math that extend far back in time. One could make a strong argument that the majority of Computer Science is not even really about computers. This is perhaps best exemplified in this quote by Edsger Dijkstra, “Computer Science is no more about computers than astronomy is about telescopes.”[8] Instead, Computer Science is about ALGORITHMS. An algorithm is a formal specification for stating a method to solve a problem. The term itself is a distortion of the name al-Khwārizmī. He was Persian mathematician who lived in the 11th century and wrote Treatise on Demonstration of Problems of Algebra, the most significant treatise on algebra written before modern times. He also wrote On the Calculation with Hindu Numerals, which presented systematic methods of applying arithmetic to algebra.

One can go even further back in time depending on how flexibly we use the term computation. Devices for facilitating arithmetic could be considered. That would push things back to around 2400 BCE. Mechanical automata for use in astronomy have also existed for many centuries. However, we will focus our attention on more complete computational devices, those that can be programmed to perform a broad range of different types of computation. In that case, the first real mechanical computer design would have been the Analytical Engine which was designed by Charles Babbage and first described in 1837. Ada Lovelace is often referred to as the first programmer because her notes on the Analytic Engine included what would have been a program for the machine. For various reasons, this device was never built and as such, the first complete computers did not come into existence for another 100 years.

It was in the 1940s that computers in a form that we would recognize them today came into existence. This began with the Zuse Z3 which was built in Germany in 1941. By the end of the 1940s there were quite a few digital computers in operation around the world including the ENIAC, built in the US in 1946. The construction of these machines was influenced in large part by more theoretical work that had been done a decade earlier.

One could argue that the foundations of the theoretical aspects of Computer Science began in 1931 when Kurt Gödel published his incompleteness theorem. This theorem, which proved that in any formal system of sufficient complexity, including standard set theory of mathematics, would have statements in it that could not be proved or disproved. The nature of the proof itself brought in elements of computation as logical expressions were represented as numbers and operations were transformations on those numbers. Five years later, Alan Turing and Alonzo Church created independent models of what we now consider to be computation. In many ways, the work they did in 1936 was the true birth of Computer Science as a field and it enabled that first round of digital computers.

Turing created a model of computation called a Turing machine. The Turing machine is remarkably simple. It has an infinite tape of symbols and a head that can read or write on the tape. The machine keeps track of a current state, which is nothing more than a number. The instructions for the machine are kept in a table. There is one row in the table for each allowed state. There is one column for each allowed symbol. The entries in the table give a symbol to write to the tape, a direction to move the tape, and a new state for the machine to be in. The tape can only be moved one symbol over to the left or right or stay where it is at each step. Cells in the table can also say stop in which case the machine is supposed to stop running and the computation is terminated.

The way the machine works is that you look up the entry in the table for the current state of the machine and symbol on the tape under the head. You then write the symbol from the table onto the tape, replacing what had been there before, move the tape in the specified direction, and change the state to the specified state. This repeats until the stop state is reached.

At roughly the same time that Turing was working on the idea of the Turing machine, Church developed the lambda calculus. This was a formal, math-based way of expressing the ideas of computation. While it looks very different from the Turing machine, it was quickly proved that the two are equivalent. That is to say that any problem you can solve with a Turing machine can be solved with the lambda calculus and the other way around. This led to the so-called Church-Turing thesis stating that anything computable can be computed by a Turing machine or the lambda calculus, or any other system that can be shown to be equivalent to these.

### 1.2 Hardware

When we talk about computers it is typical to break the topic into two parts, hardware and software. Indeed, the split goes back as far as the work of Babbage and Lovelace. Babbage designed the hardware and focused on the basic computational abilities that it could do. Lovelace worked on putting together groups of instructions for the machine to make it do something interesting. Her notes indicate that she saw the further potential of such a device and how it could be used for more than just doing calculations.

This split still exists and is significant because most of this book focuses exclusively on one half of the split, software. To understand the software that is helpful to have at least some grasp of the hardware. If you continue to study Computer Science, hopefully you will, at some point, have a full course that focuses on the nature of hardware and the details of how it works. For now, our goal is much simpler. We want you to have a basic mental image of how the tangible elements of a computer work to make the instructions that we type in execute to give us the answers that we want.

Modern computers work by regulating the flow of electricity through wires. Most of those wires are tiny elements that have been etched into silicon and are only tens of nanometers across. The voltage on the wires is used to indicate the state of a bit, a single element of storage with only two possible values, on or off. The wires connect up transistors that are laid out in a way that allows logical processing. While a modern computer processor will include literally hundreds of millions of transistors, into the billions, we can look at things at a much higher level and generally ignore that existence of those individual wires and transistors.

In general, modern computers are built on the von Neumann architecture with minor modifications. John von Neumann was another one of the fathers of computing. One of his ideas was that programs for a computer are nothing more than data and can be stored in the same place as the data. This can be described quite well with the help of the basic diagram in figure 1.1. There is a single memory that stores both the programs and the data used by the program. It is connected to a Central Processing Unit (CPU) by a bus. The CPU, which can be more generally called a processor, has the ability to execute simple instructions, read from memory, and write to memory. When the computer is running, the CPU loads an instruction from memory, executes that instruction, then loads another. This happens repeatedly until the computer stops. This simple combination of a load and execute is called a cycle.

One of the things the CPU does is to keep track of the location in memory of the next instruction to be executed. We call a location in memory an ADDRESS. By default this moves forward each time by the appropriate amount to get to the next instruction. Different types of computers can have different instructions. All computers will have instructions to read values from memory, store values to memory, do basic math operations, and change the value of the execution address to jump to a different part of the program.

The individual instructions that computers can do are typically very simple. Computers get their speed from the fact that they perform cycles very quickly. Most computers now operate at a few gigahertz. This means that they can run through a few billion instructions every second. There are a lot of complexities to real modern computers that are needed to make that possible which are not encompassed by this simple image of a computer. In many ways, these are details that we do not have to worry about too much at the beginning, but they are important in professional programming because they can have a profound impact on the performance of a program.

We will spend just a few paragraphs talking about two of the complexities in modern
