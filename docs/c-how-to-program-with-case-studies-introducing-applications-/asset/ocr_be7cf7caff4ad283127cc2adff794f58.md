00 and continues sequentially, unless directed to some other part of the program by a transfer of control.

Use the variable accumulator to represent the accumulator register. Use the variable instructionCounter to store the number of the memory location (00 to 99) containing the instruction being performed. Use the variable operationCode to store the operation currently being performed (the instruction word’s left two digits). Use the variable operand to store the number of the memory location on which the current instruction operates. Thus, if an instruction has an operand, it’s the rightmost two digits of the instruction currently being performed. Do not execute instructions directly from memory. Rather, transfer the next instruction to be performed from memory to a variable called instructionRegister. Then “pick off” the left two digits and place them in the variable operationCode, and “pick off” the right two digits and place them in operand.

When Simpletron begins execution, the special registers are initialized as follows:

```
```
accumulator              +0000
instructionCounter          00
instructionRegister     +0000
operationCode               00
operand                     00
```
```

Now let’s “walk through” the execution of the first SML instruction, +1009 in memory location 00. This process is called an instruction execution cycle.

The instructionCounter tells us the location of the next instruction to be performed. We fetch the contents of that location from memory by using the C statement

```
```
instructionRegister = memory[instructionCounter];
```
```

The operation code and the operand are extracted from the instruction register by the statements

```
```
operationCode = instructionRegister / 100;
operand = instructionRegister % 100;
```
```

Now the Simpletron must determine that the operation code is actually a *read* (versus a *write*, a *load*, and so on). A switch statement differentiates among the twelve operations of SML. The switch simulates the behavior of various SML instructions as follows (we leave the others to the reader):

```
```
read:        scanf("%d", &memory[operand]);
load:        accumulator = memory[operand];
add:         accumulator += memory[operand];
Various branch instructions: We’ll discuss these shortly.
halt:        This instruction prints the message
             *** Simpletron execution terminated ***
```
```

then prints the name and contents of each register as well as the complete contents of all 100 memory locations. Such a printout is often called a computer dump. To help you program your dump function, the output below shows a sample dump: