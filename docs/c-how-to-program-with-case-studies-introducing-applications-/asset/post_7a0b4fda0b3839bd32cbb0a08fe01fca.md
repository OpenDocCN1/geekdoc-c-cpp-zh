
- **type** is a character indicating the symbol’s type—'C' for a constant, 'L' for a line number, or 'V' for a variable.

- **location** contains the Simpletron memory location (**00 to 99**) associated with the symbol. Simpletron memory is an array of 100 integers in which SML instructions and data are stored. For a **line number**, the location is the Simpletron memory array element at which the Simple statement’s SML instructions begin. For a **variable or constant**, the location is the Simpletron memory array element that stores the variable or constant. **Variables and constants** are allocated from location 99 of the Simpletron’s memory downward. The first variable or constant is stored in location 99, the next in location 98, and so on.

The **symbol table** plays an integral part in converting Simple programs to SML. We learned in Exercise 7.28 that an **SML instruction** is a signed four-digit integer that comprises two parts—the **operation code** and the **operand**. The operation code is determined by the Simple command. For example, the **Simple command input** corresponds to **SML operation code 10** (*read*), and the **Simple command print** corresponds to **SML operation code 11** (*write*). The operand is a **memory location** containing the **data** on which the operation code performs its task. For instance, the **operation code 10** reads a value from the keyboard and stores it in the memory **location** specified by the operand. The compiler searches symbolTable to determine the **Simpletron memory location** for each symbol so the corresponding location can be used to **complete the SML instructions**.

Each Simple statement’s compilation process is based on the particular command. For example, after the line number in a **rem statement** is inserted in the symbol table, the compiler ignores the statement’s remainder—a rem statement is for documentation purposes only—no SML code is generated. The **input, print, goto and end** statements correspond to the SML **read, write, branch** (to a specific location) and **halt** instructions. The compiler converts statements containing these Simple commands directly to SML. A **goto statement** may initially contain an **unresolved reference** if the specified **line number** refers to a statement later in the Simple program file. This is called a **forward reference**.

When a **goto statement** is compiled with an **unresolved reference**, the SML instruction must be **flagged** to indicate that the compiler’s **second pass** must complete the instruction. The flags are stored in a 100-element array int flags, in which each element is initialized to -1. If the memory location to which a line number refers is not yet known (that is, it’s not in the symbol table), its line number is stored in array flags in the element with the same subscript as the **incomplete instruction**. The incomplete instruction’s operand is set temporarily to 00. For example, an unconditional branch instruction (making a **forward reference**) is left as +4000 until the compiler’s second pass, which we’ll describe shortly.

Compiling an **if...goto** or **if...goto** statement is more complicated than other statements—each produces more than one SML instruction. For an **if...goto** statement, the compiler produces code to test the condition and possibly branch to another line. The result of the branch could be an unresolved forward reference. Each Simple relational and equality operator can be simulated using SML’s *branch zero* and *branch negative* instructions (or possibly a combination of both).

For a **let** statement, the compiler produces code to evaluate an **arbitrarily complex** infix arithmetic expression consisting of operators, single-letter integer variable names, integer constants and possibly parentheses. Expressions should separate each operand and operator with a space. Exercises 12.22–12.23 presented the **infix-to-postfix conversion algorithm** and the **postfix-evaluation algorithm** compilers use to evaluate expressions. Before building your compiler, you should complete those exercises. The compiler converts each expression from **infix notation** to **postfix notation**, then evaluates the **postfix expression**. As you’ll see, the compiler actually generates machine-language instructions in the process of performing the postfix expression evaluation.

How is it that the compiler produces the **machine language** to evaluate an **expression containing variables**? The **postfix-evaluation algorithm** contains a “hook” that allows our compiler to generate SML instructions rather than actually evaluating the expression. To enable this “hook” in the compiler, the **postfix-evaluation algorithm** must be modified to:

- **search the symbol table** for each symbol it encounters (and possibly insert it),
- determine the symbol’s corresponding **memory location**, and
- **push the memory location instead of the symbol onto the stack**.

When an operator is encountered in the **postfix expression**, the stack’s top two **memory locations** are popped, and SML for effecting the operation is produced using the **memory locations** as operands. Each subexpression’s result is stored in a **temporary memory location** and pushed back onto the stack, so the **postfix expression**’s evaluation can continue. When **postfix evaluation** is complete, the **result’s memory location** is the only location left on the stack. This is popped, and SML instructions are generated to assign the result to the variable at the left of the **let** statement.

## Second Pass

The compiler’s second pass performs two tasks:

- resolve any unresolved references, and
- output the SML code to a file.

Resolution of each reference occurs as follows:

- 1. Search the **flags** array for an **unresolved reference** (i.e., an element with a value other than –1).
- 2. Locate the structure in array **symbolTable** containing the symbol stored in the **flags** array (be sure that the type of the symbol is **‘L’ for line number**).
- 3. Insert the memory location from structure member **location** into the instruction with the unresolved reference (remember that an instruction containing an unresolved reference has operand **00**).
- 4. Repeat *Steps 1–3* until the end of the **flags** array is reached.

After the resolution process is complete, the compiler outputs the SML code to a file with one SML instruction per line. The Simpletron can read this file and execute its instructions (after the simulator is modified to read its input from a file, of course).

### A Complete Example

The following example illustrates a complete conversion of a Simple program to SML. Consider a Simple program that inputs an integer, sums the values from 1 to that integer and prints that sum. So, if the user enters 4, the program would calculate 1 + 2 + 3 + 4, which is 10 and print that value. Figure 12.8 shows the program and the SML instructions produced by the compiler’s first pass. Figure 12.9 shows the symbol table constructed by the compiler’s first pass. Figure 12.10 shows how the compiler allocates Simpletron memory downward from cell 99. In a moment, we’ll do a step-by-step walkthrough showing precisely how the compiler creates these tables.

| Simple program | SML location and instruction | Description |
| --- | --- | --- |
| 5 rem    sum 1 to x | *none* | rem ignored |
| 10 input x | 00 +1099 | read x into location 99 |
| 15 rem    check y === x | *none* | rem ignored |
| 20 if y === x goto 60 | 01 +2098 | load y (location 98) into accumulator |
|  | 02 +3199 | sub x (location 99) from accumulator |
|  | 03 +4200 | branch zero to unresolved location |
| 25 rem    increment y | *none* | rem ignored |
| 30 let y = y + 1 | 04 +2098 | load y (location 98) into accumulator |
|  | 05 +3097 | add 1 (location 97) to accumulator |
|  | 06 +2196 | store in temporary location 96 |
|  | 07 +2096 | load from temporary location 96 |
|  | 08 +2198 | store accumulator in y (location 98) |
| 35 rem    add y to total t | *none* | rem ignored |
| 40 let t = t + y | 09 +2095 | load t (location 95) into accumulator |
|  | 10 +3098 | add y (location 98) to accumulator |
|  | 11 +2194 | store in temporary location 94 |
|  | 12 +2094 | load from temporary location 94 |
|  | 13 +2195 | store accumulator in t (location 95) |
| 45 rem    loop to y === x test | *none* | rem ignored |
| 50 goto 20 | 14 +4001 | branch to location 01 |
| 55 rem    output result | *none* | rem ignored |
| 60 print t | 15 +1195 | output t (location 95) to screen |
| 99 end | 16 +4300 | terminate execution |

**Fig. 12.8** | SML instructions produced after the compiler’s first pass.
