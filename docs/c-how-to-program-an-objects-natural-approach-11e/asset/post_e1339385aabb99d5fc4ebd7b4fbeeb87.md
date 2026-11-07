
is tokenized, the line number 30 is inserted in the symbol table as type 'L' and assigned SML location 04. Command `let` indicates that the line is an assignment statement. First, all the symbols on the line are inserted in the symbol table (if they are not already there). The constant integer 1 is inserted as type C and assigned SML location 97. Next, the right side of the assignment is converted from infix to postfix notation. Then the postfix expression `(y 1 +)` is evaluated. Symbol y is located in the symbol table, and its corresponding memory location, 98, is pushed onto the stack. Symbol 1 is also located in the symbol table, and its corresponding memory location, 97, is pushed onto the stack. When the operator + is encountered, the postfix evaluator pops the stack into the right operand of the operator and pops the stack again into the left operand of the operator, then produces the SML instructions

```
04 +2098    (load y)
05 +3097    (add 1)
```

The result of incrementing y is stored in a **temporary location in memory** (96) with instruction

```
06 +2196    (store temporary)
```

and the temporary location is **pushed onto the stack**. Now that the expression has been evaluated, the result must be stored in the let statement's variable y. So, the temporary location is loaded into the accumulator, and the accumulator is stored in y with the instructions

```
07 +2096    (load temporary)
08 +2198    (store y)
```

Notice that some of these SML instructions—storing the accumulator into temporary location 96, then immediately reloading the accumulator from location 96—appear to be **redundant**. Eliminating such redundancy is an example of compiler optimization, which we'll say more about shortly.

## Compiling Line 35

When the compiler tokenizes the statement

```
35 rem   add y to ytotal
```

it inserts line number 35 in the symbol table as type 'L' and assigns it location 09.

## Compiling Line 40

The following statement is similar to line 30:

```
40 let t = t + y
```

The variable t is inserted in the symbol table as type 'V' and assigned SML location 95. The instructions follow the same logic and format as line 30, and the instructions

```
09 +2095
10 +3098
11 +2194
12 +2094
13 +2195
```

are generated. The result of t + y is assigned to temporary location 94 before being assigned to t (95). The instructions in memory locations 11 and 12 also appear to be redundant. Again, we’ll discuss this optimization issue shortly.

## Compiling Line 45

The statement

```
45 rem    loop to y == x test
```

is a remark, so line 45 is inserted in the symbol table as type 'L' and assigned SML location 14.

## Compiling Line 50

The statement

```
50 goto 20
```

transfers control to line 20. Line number 50 is inserted in the symbol table as type 'L' and assigned SML location 14. The equivalent of goto in SML is the unconditional branch (40) instruction that transfers control to a specific SML location. The compiler searches the symbol table for line 20 and finds that it corresponds to SML location 01. The operation code (40) is multiplied by 100, and location 01 is added to produce the instruction +4001 at location 14.

## Compiling Line 55

The statement

```
55 rem    output result
```

is a remark, so line 55 is inserted in the symbol table as type 'L' and assigned SML location 15.

## Compiling Line 60

The statement

```
60 print t
```

is an output statement. Line number 60 is inserted in the symbol table as type 'L' and assigned SML location 15. The SML equivalent of print is operation code 11 (write). Variable t’s location is determined from the symbol table, then added to the result of multiplying the operation code by 100. This forms the instruction +1195 at location 15.

## Compiling Line 99

The statement

```
99 end
```

is the final line of the program. Line number 99 is stored in the symbol table as type 'L' and assigned SML location 16. The end command produces the SML instruction +4300 (43 is halt in SML). This is written as the final instruction in the SML memory array. The halt instruction has no operand.

## The Compilation Process’s Second Pass

On the compiler’s *second pass*, we begin by searching the *flags array* for values other than -1. Location 03 contains 60, so the compiler knows that instruction 03 is incomplete. The compiler completes the instruction by searching the symbol table for 60, determining its location and adding the location to the incomplete instruction. In this case, the search determines that line 60 corresponds to SML location 15, so the compiler completes the instruction at location 03, replacing +4200 with +4215. The Simple program has now been compiled successfully.

## Building Your Compiler

To build the compiler, you’ll have to perform each of the following tasks:

- a) Modify the Simpletron simulator program you wrote in Exercise 7.10 to take its input from a file specified by the user (see Chapter 8). The simulator should also output its results to a file in the same format as the screen output.
- b) Modify the infix-to-postfix evaluation algorithm of Exercise 13.29 to process multi-digit integer operands and single-letter variable-name operands. Class `std::string`’s `find` and `substr` functions can be used to locate each constant and variable in an expression. Constants can be converted from strings to integers using the `<string>` header’s `stoi` function. The postfix expression’s data representation must be altered to support variable names and integer constants.
- c) Modify the postfix evaluation algorithm to process multi-digit-integer operands and single-letter variable-name operands. The algorithm should now implement the previously discussed “hook” so that it produces SML instructions rather than directly evaluating the expression. Class `std::string`’s `find` and `substr` functions can be used to locate each constant and variable in an expression, and constants can be converted from strings to integers using the `<string>` header’s `stoi` function. The data representation of the postfix expression must be altered to support variable names and integer constants.
- d) Build the compiler—incorporate Part b and Part c for evaluating expressions in `let` statements. Your program should contain a function that performs the compiler’s first pass and one that performs its second pass.

## 13.33 (Optimizing the Simple Compiler)

When a program is compiled and converted into SML, a set of instructions is generated. Certain combinations of instructions often repeat themselves, often in triplets called productions. A production normally consists of three instructions such as *load*, *add* and *store*. For example, here are five of the unoptimized SML instructions produced while compiling the program in Fig. 13.13:

```
04 +2098    (load)
05 +3097    (add)
06 +2196    (store)
07 +2096    (load)
08 +2198    (store)
```

The first three instructions are the production that adds 1 to y. Instructions 06 and 07 store the accumulator value in temporary location 96, then load the value from that location right back into the accumulator so instruction 08 can store the value in location 98. Often a production is followed by a load instruction for the same location that was just stored. This code can be optimized by eliminating the store instruction and the subsequent load instruction that operate on the same memory location. This optimization would decrease the SML program’s “memory footprint” by 25% and improve its execution speed. Figure 13.16 shows the **optimized SML** for the program of Fig. 13.13. There are **four fewer** instructions in the optimized code. Modify your compiler to perform the optimization you learned in this exercise.

| Simple program | SML location and instruction | Description |
|---|---|---|
| 5 rem sum 1 to x | *none* | rem ignored |
| 10 input x | 00 &nbsp; +1099 | read x into location 99 |
| 15 rem &nbsp; check y == x | *none* | rem ignored |
| 20 if y == x goto 60 | 01 &nbsp; +2098 | load y (98) into accumulator |
|  | 02 &nbsp; +3199 | sub x (99) from accumulator |
|  | 03 &nbsp; +4211 | branch to location 11 if zero |
| 25 rem &nbsp; increment y | *none* | rem ignored |
| 30 let y = y + 1 | 04 &nbsp; +2098 | load y into accumulator |
|  | 05 &nbsp; +3097 | add 1 (97) to accumulator |
|  | 06 &nbsp; +2198 | store accumulator in y (98) |
| 35 rem &nbsp; add y to total | *none* | rem ignored |
| 40 let t = t + y | 07 &nbsp; +2096 | load t from location (96) |
|  | 08 &nbsp; +3098 | add y (98) to accumulator |
|  | 09 &nbsp; +2196 | store accumulator in t (96) |
| 45 rem &nbsp; loop to y == x test | *none* | rem ignored |
| 50 goto 20 | 10 &nbsp; +4001 | branch to location 01 |
| 55 rem &nbsp; output result | *none* | rem ignored |
| 60 print t | 11 &nbsp; +1196 | output t (96) to screen |
| 99 end | 12 &nbsp; +4300 | terminate execution |

**Fig. 13.16**  Optimized code for the program of Fig. 13.13.

## 13.34 (Enhancing the Simple Compiler)

Perform the following modifications to the Simple compiler. Some of these may also require modifications to the Simpletron Simulator program you wrote in Exercise 7.10. Many of these are quite challenging and could require substantial effort.

- a) Modify the Simpletron’s memory to have 1000 cells (000–999). Modify the compiler to generate machine language appropriate for the 1000-element Simpletron memory.
- b) Allow the compiler to process floating-point values in addition to integers. The Simpletron Simulator must also be modified to process floating-point values.
- c) Add support for **unary minus** to specify negative integer values.
- d) Allow the **modulus operator (%)** to be used in let statements. Modify the Simpletron Machine Language to include a modulus instruction.
- e) Allow **exponentiation** in a let statement using ^ as the exponentiation operator. Modify the Simpletron Machine Language to include an exponentiation instruction.
