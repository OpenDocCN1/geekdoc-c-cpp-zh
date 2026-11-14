
- Insert/delete at the end
  The insert and delete operations at the end of the array in either mode are done in constant time. No elements need be moved; thus, the complexity is O(1).

- Insert/delete in the middle
  The operation comprises two pieces: finding the element then performing the insert or delete. The array supports random access; thus, finding the element is a constant time operation. In the overwrite mode, inserting an element is also done in constant time. The complexity is O(1).

  In the insert mode, all elements below (with higher index) must be moved to make room for the new element. For the two boundary cases, we only move a single element, or we move all elements but one. Thus, the complexity is, on average, O(N/2), or simply O(N), where N is the number of elements that need to be moved.

  The complexity of the delete operation is the same as that for the insert mode for both the boundary and typical cases, O(N).

- Access at the beginning, the end, and in the middle.
  These accesses are all constant time operations since the array supports random access.

### 14.9.2 Linked List

- Insert/delete at the beginning
  Inserting or deleting a link at the head of a linked list involves the modification of a couple of addresses. These operations are independent of the size of the list; thus, the complexity is O(1).

- Insert/delete at the end
  For either of these operations, two cases must be considered. If a reference to the tail of the linked list is maintained, then either operation can be completed in constant time.

  On the other hand, if only the head reference is retained, then one must first find the tail of the list. Such an operation depends on the number of elements in the list; thus, the complexity in such a case is O(N), where N is the size of the container.

- Insert/delete in the middle
  The operation comprises two pieces: finding the element and performing the insert or delete. The linked list does not support random access; thus, finding the element depends on the number of elements in the list. Like the delete at the end, the access is of order N and the insert or delete is constant. Thus, either of these operations has complexity O(N).

- Access at the beginning, the end, and in the middle
  Like insert or delete in the beginning, the end, or the middle of the linked list, the time complexity is controlled by the amount of time to find the element. Thus, either of these operations will have complexity that is the same as the corresponding insert or delete operations.

## 14.10 INSTRUCTIONS IN DETAIL

We have looked at order of magnitude measures and comparisons for algorithms. Eventually, the code must be written, compiled, and run on the microprocessor. In real-time systems, this is where the interesting design issues and challenges arise. In a hard real-time system, a few nanoseconds can mean the difference between success and failure of a design.

We will now move inside of the algorithm to examine the temporal performance of each of the instructions in detail. As with any other tools and approaches that one is working with, the tools, the problem, and the context must be thoroughly understood. Analyzing individual instructions or sequences of instructions, which will be done shortly, is most definitely not appropriate for an entire program. Rather, the technique is used and applied to understand and to optimize a critical set of instructions.

Once again, we assume that a program or algorithm is made up of several common flow of control constructs. The basic constructs will be analyzed in detail; these components can be combined later as needed.
Several additional caveats are in order.

1. Single thread of execution is assumed.
2. The analysis is conducted at the assembly language level. Each different compiler is going to generate somewhat different assembly code, even for the same target. The analysis must be based on the compiler that is generating the final code for the microprocessor used in the design.
3. Compilers support different options for the compilation process. Such variations include the size of the target memory. Different code may be generated for a small memory model versus a large memory model.

Consistency is the key word. Always perform the analysis on the code that will ultimately be embedded in the system being designed.

### 14.10.1 Getting Started

After the high-level code to be analyzed is identified, the analysis is conducted on the assembly language listing. Most contemporary compilers will not generate such a listing automatically. However, the option to do so is generally available. Once one has a complete assembly listing, the specific instructions that are of interest can be identified.

From the processor vendor's assembly language manuals, one can then determine the time for each instruction. This time can vary with any of the following.

- Addressing mode of instruction.
- The piece of memory from which the instruction or data must be fetched:
  - Immediate
  - Register
  - Primary
  - Secondary

When computing times, it may be necessary to use minimum, maximum, or average numbers depending upon the objective at hand. For example, is one looking for the longest path or the shortest? Is the objective to meet a deadline, or is it to ensure that a value doesn't change too quickly?

### 14.10.2 Flow of Control

As the design and implementation of increasingly complex embedded systems continue, it is not going to be possible to develop a solution based on executing a few lines of code. Rather, the designs are going to be implemented as collections of cooperating tasks and threads. Some of the tasks will be scheduled according to a predetermined algorithm, whereas others will be invoked asynchronously in response to internal or external events. The invocation of each new task or thread will entail a change from a current context to a new one and may involve saving the current context and retrieving an old one. Depending on the tasks to be performed, such a series of operations will take varying amounts of time and can be critical in a real-time system. To be able to effectively design embedded systems, one must thoroughly understand the flow of control both inside and outside of the system. Essential to such an understanding is the ability to analyze, in time, the flow of control through the system.

The flow of control – the single-threaded path of execution – through most contemporary programs can be modeled and analyzed as a composite of four basic elements:

- Sequential
- Branch
- Loop
- Function call.

### big-O

We have already analyzed each of these constructs from a big-O or order of magnitude perspective. We will now examine them, first from a C language level and then in greater detail at the assembler level.

### 14.10.2.1 Sequential

A sequential block is a set of instructions each of which is executed in sequence – that is, in the order that the instructions appear in the program and ultimately in program memory, our firmware. Such a set of instructions may include declarations, definitions, or assignments (Figure 14.10).

![](img/679b8d2d47f1bf86e17aca48f596f5cc_727_0.png)

### 14.10.2.2 Branch

A branch is the simplest construct that allows the flow of a thread of execution through the program to be altered. One of several branches can be selected based on some condition. Graphically, this type of construct is seen in Figure 14.11 and appears in high-level code as statements such as:

![](img/679b8d2d47f1bf86e17aca48f596f5cc_727_1.png)

```
if else
switch or case
```

In the assembler, the branch will be implemented as a series of jump or branch instructions, depending on the assembler.

### 14.10.2.3 Loop

The _loop_ construct expresses a set of instructions that is repeatedly executed until some termination condition is met. As the diagram in Figure 14.12 illustrates, a decision about whether to execute the code block can be made before entering the loop – the code may not be executed – or after the loop – the code is executed at least once.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_728_0.png)

Figure 14.12 The Loop.

A construct of this type is seen in high-level instructions of the form:

```
do or repeat
while
for
```

and in the assembler as a coordinated collection of jumps.

### 14.10.2.4 Function Call

The most complex flow of control component is the function call. In this component, the current context is exited, a set of instructions is executed in a new context, and then flow returns to the initial context. Such a construct can be found in a

```
Function, Procedure or Subroutine call
Interrupt Handler and Interrupt Service Routine
Co-Routine
```

Context is interpreted as the information that characterizes the current executing environment of the program and includes items such as

- Program counter
- Auto variables
- Register contents
- State of globals.

The flow of control is illustrated in Figure 14.13.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_728_1.png)

Figure 14.13 The Function Call.
