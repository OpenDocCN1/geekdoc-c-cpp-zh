
### Sample SML Program That Adds Two Numbers

Let’s consider several simple SML programs. The following SML program reads two numbers from the keyboard, then computes and prints their sum:

| Location | Number | Instruction |
|---|---|---|
| 00 | +1007 | (Read A) |
| 01 | +1008 | (Read B) |
| 02 | +2007 | (Load A) |
| 03 | +3008 | (Add B) |
| 04 | +2109 | (Store C) |
| 05 | +1109 | (Write C) |
| 06 | +4300 | (Halt) |
| 07 | +0000 | (Variable A) |
| 08 | +0000 | (Variable B) |
| 09 | +0000 | (Result C) |

The instruction +1007 reads the first number from the keyboard and places it into location 07. Then +1008 reads the next number into location 08. The *load* instruction, +2007, copies the first number into the accumulator. The *add* instruction, +3008, adds the second number to the number in the accumulator. *All SML arithmetic instructions leave their results in the accumulator.* The *store* instruction, +2109, copies the result from the accumulator into memory location 09, from which the *write* instruction, +1109, then takes the number and prints it as a signed four-digit decimal number to the screen. The *halt* instruction, +4300, terminates execution.

### Sample SML Program That Determines the Largest of Two Values

The next SML program reads two numbers from the keyboard, then determines and prints the larger value:

| Location | Number | Instruction |
|---|---|---|
| 00 | +1009 | (Read A) |
| 01 | +1010 | (Read B) |
| 02 | +2009 | (Load A) |
| 03 | +3110 | (Subtract B) |
| 04 | +4107 | (Branch negative to 07) |
| 05 | +1109 | (Write A) |
| 06 | +4300 | (Halt) |
| 07 | +1110 | (Write B) |
| 08 | +4300 | (Halt) |
| 09 | +0000 | (Variable A) |
| 10 | +0000 | (Variable B) |

The instruction +4107 is a conditional transfer of control, like an if statement.

Now write SML programs to accomplish each of the following tasks.

- a) Use a sentinel-controlled loop to read positive integers, then compute and print their sum.
- b) Use a counter-controlled loop to read seven numbers, some positive and some negative. Compute and print their average.
- c) Read a series of numbers. Determine and print the largest number. The first number read indicates how many numbers should be processed.

## 7.10 (A Computer Simulator)

It may at first seem outrageous, but in this exercise you’ll build your own computer. No, you won’t be soldering components together. Rather, you’ll use the powerful technique of software-based simulation to create a software model of the Simpletron. You will not be disappointed. Your Simpletron simulator will turn the computer you’re using into a Simpletron, and you’ll actually be able to run, test and debug the SML programs you wrote in Exercise 7.9!

When you run your Simpletron simulator, it should begin by printing:

```text
***                 Welcome to Simpletron                 ***
***                                                       ***
*** Please enter your program one instruction           ***
*** (or data word) at a time. I will type the           ***
*** location number and a question mark (?).            ***
*** You then type the word for that location.           ***
*** Type the sentinel -99999 to stop entering           ***
*** your program.                                        ***
```

Simulate the memory of the Simpletron with a 100-element one-dimensional array memory. Now assume that the simulator is running, and let’s examine the dialog as we enter the program of Example 2 of Exercise 7.9:

```text
00 ? +1009
01 ? +1010
02 ? +2009
03 ? +3110
04 ? +4107
05 ? +1109
06 ? +4300
07 ? +1110
08 ? +4300
09 ? +0000
10 ? +0000
11 ? -99999
*** Program loading completed ***
*** Program execution begins  ***
```

The SML program has now been placed (or loaded) into the array memory. Next, the Simpletron executes the SML program. It begins with the instruction in location 00 and continues sequentially unless directed to some other part of the program by a transfer of control.

Use the variable `accumulator` to represent the accumulator register. Use the variable `instructionCounter` to store the number of the memory location (00 to 99) containing the instruction being performed. Use the variable `operationCode` to store the operation currently being performed (the instruction word’s left two digits). Use the variable `operand` to store the number of the memory location on which the current instruction operates. Thus, if an instruction has an operand, it’s the rightmost two digits of the instruction currently being performed. Do not execute instructions directly from memory. Rather, transfer the next instruction to be performed from memory to a variable called `instructionRegister`. Then “pick off” the left two digits and place them in the variable `operationCode`, and “pick off” the right two digits and place them in `operand`.

When Simpletron begins execution, the special registers are initialized as follows:

| Register | Initial value |
|---|---:|
| `accumulator` | `+0000` |
| `instructionCounter` | `00` |
| `instructionRegister` | `+0000` |
| `operationCode` | `00` |
| `operand` | `00` |

Now let’s “walk through” the execution of the first SML instruction, +1009 in memory location 00. This process is called an instruction execution cycle.

The `instructionCounter` tells us the location of the next instruction to be performed. We fetch the contents of that location from memory by using the C statement

```
instructionRegister = memory[instructionCounter];
```

The operation code and the operand are extracted from the instruction register by the statements

```
operationCode = instructionRegister / 100;
operand = instructionRegister % 100;
```

Now the Simpletron must determine that the operation code is actually a `read` (versus a `write`, a `load`, and so on). A switch statement differentiates among the twelve operations of SML. The switch simulates the behavior of various SML instructions as follows (we leave the others to the reader):

- `read`:

  ```cpp
  cin >> memory[operand];
  ```

- `load`:

  ```cpp
  accumulator = memory[operand];
  ```

- `add`:

  ```cpp
  accumulator += memory[operand];
  ```

- Various branch instructions: We’ll discuss these shortly.

- `halt`—This instruction prints `*** Simpletron execution terminated ***` then prints the name and contents of each register and the complete contents of all 100 memory locations. Such a printout is often called a computer dump. To help you program your dump function, the output below shows a sample dump:

```text
REGISTERS:
accumulator                         +0000
instructionCounter                    00
instructionRegister                 +0000
operationCode                          00
operand                                00

MEMORY:
       0      1      2      3      4      5      6      7      8      9
 0  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
10  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
20  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
30  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
40  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
50  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
60  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
70  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
80  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
90  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000  +0000
```

A dump after executing a Simpletron program would show the actual values of instructions and data values at the moment execution terminated. You can print leading 0s in front of an integer that is shorter than its field width by placing the `0` formatting flag before the field width in the format specifier as in `"%02d"`. You can place a `+` or `-` sign before a value with the `+` formatting flag. So to produce a number of the form `+0000`, you can use the format specifier `"%+05d"`.

Let’s proceed with the execution of our program’s first instruction, namely the +1009 in location 00. As we’ve indicated, the switch statement simulates this by performing the statement

```cpp
cin >> memory[operand];
```

A question mark (?) should be displayed on the screen to prompt the user for input. The Simpletron waits for the user to type a value and then press the Return (or Enter) key. The value is then read into location 09.

At this point, simulation of the first instruction is completed. All that remains is to prepare the Simpletron to execute the next instruction. Because the instruction just performed was not a transfer of control, we need merely increment the instruction counter register as follows:

```
++instructionCounter;
```

This completes the simulated execution of the first instruction. The entire process (i.e., the instruction execution cycle) begins anew with the fetch of the next instruction to be executed.

Now let’s consider how the branching instructions—the transfers of control—are simulated. All we need to do is adjust the value in the instruction counter appropriately. Therefore, the unconditional branch instruction (40) is simulated within the switch as

```
instructionCounter = operand;
```
