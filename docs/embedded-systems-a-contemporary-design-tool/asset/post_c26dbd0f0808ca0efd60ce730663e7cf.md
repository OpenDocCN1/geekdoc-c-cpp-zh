

## 1.17 An embedded application executing on the microprocessor in Problem 1.15 is required to perform the following computation:

Z = W₁×Y₁ + W₂×Y₂ + W₃×Y₃

on the contents of memory locations Z₁, W₁, Y₁, W₂, Y₂, W₃, and Y₃. None of the contents of locations W or Y may be destroyed.

- (a) Write a straight-line program for the task described above.
- (b) Write a loop program for the same task on the same computer.
- (c) Calculate the number of main memory accesses (Read or Write operations) required for each program. Include all accesses required for fetching and executing the instructions. For example, the instruction:

```
MOVE Ri, Rj
```

requires two memory accesses: one for reading the instruction from main memory into the microprocessor and one for reading the operand from main memory location contained in Ri into the microprocessor.

## 1.18 In some computers, subroutine linkage is implemented in the following way. The call subroutine instruction stores the return address (the next instruction in the calling program) in the first location of the subroutine and then branches to the second location, where the execution of the subroutine begins.

- (a) Define a suitable instruction for returning from the subroutine.
- (b) How would you pass parameters between the calling program and the subroutine?
- (c) Would the above linkage support nesting of subroutines? Why or why not?
- (d) Would the above linkage support recursion? Why or why not?

## 1.19 Based on the RTL model of a microprocessor datapath given in Figure 1.52 and the RTL operations given in Table 1.4, please identify the necessary steps that comprise each phase of the instruction cycle in order to perform the following instruction on that microprocessor:

```
// add the contents of the value
// contained in the register R3 to
// the contents of the memory
// location pointed to by R2 and
// put the results into R4.
add R4, R3, *R2;
```

## 1.20 We have the following C code fragment that adds one to each element of an array.

```
int a[4] = { 1, 2, 3, 4 }; // declare an array
// of integers
for i ;
for ( i = 0; i < 4; i++)
a[i] = a[i] + 1; // add to each
// element of the array
```

- (a) Using the instructions you developed in Problem 1.15 translate the given code fragment into assembler.
- (b) Using the RTL operations given in Table 1.4, translate the assembler to RTL level.
- (c) Using the instructions you developed in Problem 1.15 and the assembler from part (a), translate the code fragment into machine code.

## 1.21 The architecture known as the Aiken or Harvard architecture uses a separate data memory and a separate instruction memory.

- (a) Please give two advantages and two disadvantages of the Harvard architecture in comparison to the Princeton architecture. Be precise in your answer.
- (b) For the following C++ code fragment, which memory, the instruction or the data memory, should contain the values for x and y? Please explain why.

```
int x = 3;
int y = 4;
x = x + y;
```

- (c) Using the following memory diagrams, please place the values for x and y into locations in the appropriate memory.*

| | Instruction memory | |
|---|---|---|
| Memory location | Memory address | Contents |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |

| | Data memory | |
|---|---|---|
| Memory location | Memory address | Contents |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |

| | Data memory | |
|---|---|---|
| Memory location | Memory address | Contents |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |

- (d) Are the following assembly code instructions one-, two-, or three-address instructions? Please explain your answer.

```
LOADI Ri, #constant // load the constant
                    // into Ri
LOADI *Ri, #constant // load the constant
                     // into what Ri is
                     // pointing to
ADD2 Ri, Rj         // add the contents of
                    // Ri to Rj and place
                    // the result in Ri
ADD2 *Ri, *Rj       // add the contents of
                    // what Ri is pointing to
                    // to what Rj is pointing to
                    // and place the result in
                    // what Ri is pointing to
```

- (e) Using the instructions above, complete the following code fragment to implement the addition operation in part (b).

| LOADI | | |
|---|---|---|
| LOADI | | |
| ADD2 | | |

- (f) Using the following memory diagrams, please place the instructions you wrote in part (e) into locations in the appropriate memory.

| | Instruction memory | |
|---|---|---|
| Memory location | Memory address | Contents |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |
| | | |

- (g) Please provide a format for the add instruction given above. Explain the purpose of each field in your implementation.
- (h) Please identify all of the steps necessary to execute the add instruction in part (e) above on the Harvard machine. Refer to the specific parts of the architecture diagram in your descriptions.

## 1.22 A computer is designed that uses a set of special registers, R50-R53, rather than the stack to pass data into and out of a subroutine. The stack is only used to hold the return address. The stack pointer is held in the special register SP and the program counter in register PC. The machine has four general-purpose registers R0-R3. The machine has a status flag, equal, that is approximately set or reset for each instruction execution as indicated below. Write a routine exp(num, pow) that will compute num^pow for such a machine and return that value.

- (a) Please write the detailed level pseudocode for invoking such a routine assuming that it is called from some higher level function. Be certain to identify all of the steps.
- (b) Please write the sequence of assembly language steps necessary to implement such a sequence using the following instructions.

```
LOAD Ri, Rj     // Ri <- Rj, sets the equal
                // flag true if Ri contains 0
LOAD Ri, #val   // Ri <- #val, sets the
                // equal flag true if Ri
                // contains 0
BE @Ri          // jumps to address
                // contained in Ri if the
                // equal flag is true
BNE @Ri         // jumps to address
                // contained in Ri if the
                // equal flag is false
MUL Ri, Rj      // Ri <- Ri * Rj, sets the
                // equal flag true if Ri
                // contains 0
DIV Ri, Rj      // Ri <- Ri / Rj, sets the
                // equal flag true if Ri
                // contains 0
```

```
ADD2 Ri, Rj    // Ri <- Ri + Rj, sets the
               // equal flag true if Ri
               // contains 0
```

```
PUSH Ri        // stack <- Ri
POP Ri         // Ri <- stack
```

```
SUB2 Ri, Rj    // Ri <- Ri - Rj, sets the
               // equal flag true if Ri
               // contains 0
```

```
INC Ri         // Ri <- Ri + 1
DEC Ri         // Ri <- Ri - 1, sets the
               // equal flag true if Ri
               // contains 0
```

- (e) Using a value of 20 for num and 3 for pow, please indicate the contents of each of the following registers at the execution points indicated assuming the sequence of steps you have identified was executed. Also indicate the top of the stack.

Assume the original function call is at memory address 3050 and that the subroutine is at memory address 5000.

### Prior to Function Call

| PC | |
|---|---|

| GP Registers | SP Registers | Stack |
|---|---|---|
| R0 | RS0 | |
| R1 | RS1 | |
| R2 | RS2 | |
| R3 | RS3 | |

### After the Function Call

| PC | |
|---|---|

| GP Registers | SP Registers | Stack |
|---|---|---|
| R0 | RS0 | |
| R1 | RS1 | |
| R2 | RS2 | |
| R3 | RS3 | |

### Prior to the Return

| PC | |
|---|---|

| GP Registers | SP Registers | Stack |
|---|---|---|
| R0 | RS0 | |
| R1 | RS1 | |
| R2 | RS2 | |
| R3 | RS3 | |

### After the Return

| PC | |
|---|---|

| GP Registers | SP Registers | Stack |
|---|---|---|
| R0 | RS0 | |
| R1 | RS1 | |
| R2 | RS2 | |
| R3 | RS3 | |

