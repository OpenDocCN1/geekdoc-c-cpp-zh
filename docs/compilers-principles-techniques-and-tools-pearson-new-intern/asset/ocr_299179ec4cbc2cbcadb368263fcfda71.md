# 8.3. ADDRESSES IN THE TARGET CODE

nience, we shall use positive offsets by maintaining in a register SP a pointer to the beginning of the activation record on top of the stack. When a procedure call occurs, the calling procedure increments SP and transfers control to the called procedure. After control returns to the caller, we decrement SP, thereby deallocating the activation record of the called procedure.

The code for the first procedure initializes the stack by setting SP to the start of the stack area in memory:

```
LD   SP, #stackStart                 // initialize the stack
code for the first procedure
HALT                                 // terminate execution
```

A procedure call sequence increments SP, saves the return address, and transfers control to the called procedure:

```
ADD  SP, SP, #caller.recordSize     // increment stack pointer
ST   O(SP), #here + 16               // save return address
BR   callee.codeArea                 // jump to the callee
```

The operand #caller.recordSize represents the size of an activation record, so the ADD instruction makes SP point to the next activation record. The operand #here + 16 in the ST instruction is the address of the instruction following BR; it is saved in the address pointed to by SP.

The return sequence consists of two parts. The called procedure transfers control to the return address using

```
BR   *O(SP)                          // return to caller
```

The reason for using *O(SP) in the BR instruction is that we need two levels of indirection: O(SP) is the address of the first word in the activation record and *O(SP) is the return address saved there.

The second part of the return sequence is in the caller, which decrements SP, thereby restoring SP to its previous value. That is, after the subtraction SP points to the beginning of the activation record of the caller:

```
SUB  SP, SP, #caller.recordSize     // decrement stack pointer
```

Chapter 7 contains a broader discussion of calling sequences and the trade-offs in the division of labor between the calling and called procedures.

**Example 8.4:** The program in Fig. 8.5 is an abstraction of the quicksort program in the previous chapter. Procedure *q* is recursive, so more than one activation of *q* can be alive at the same time.

Suppose that the sizes of the activation records for procedures m, p, and q have been determined to be *msize*, *psize*, and *qsize*, respectively. The first word in each activation record will hold a return address. We arbitrarily assume that the code for these procedures starts at addresses 100, 200, and 300, respectively,