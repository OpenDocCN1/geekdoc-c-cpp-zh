The subroutine FACT is on lines 32 through 93. It repeatedly calls itself passing N-1 each time until N is one at which time it returns (see line 12 in Figure 67). Since the program calls itself, it cannot use a static save area. It must allocate a new save area at each entry and delete it upon exit.

Upon entry, FACT performs the usual Store Multiple (line 33) to save the calling program's registers in the calling program's save area pointed to by R13 according to the traditional linkage convention. Lines 34 and 35 establish a local base register (R12).

Now things deviate from the usual entry sequence. First, we preserve R1, the contents of which are a pointer to the parameter list, by copying it to R3. This is necessary since the GETMAIN on line 41 returns an address in R1 of the memory allocated.

```
```asm
 1          PRINT   NOGEN
 2          EQUATES
 3 MAIN     SUBENTRY                 * LEGACY LINKAGE

 5          LA      R5,5             * FIND FACTORIAL OF 5
 6          ST      R5,N             * SAVE IN MEMORY
 7          LA      R1,PARMS          * ADDRESS OF PARM LIST

 9          L       R15,=V(FACT)     * CALL FUNCTION
10          BASR    R14,R15

12          L       R1,N             * LOAD ANSWER
13          XDECO   R1,OUT           * CVT TO DEC & PRINT
14          XPRNT   MSG,L'MSG+L'OUT
15          SR      R15,R15          * RETURN CODE
16          SUBEXIT                   * LEGACY RETURN
17          LTORG

19 PARMS    DC      A(N)             * PARM LIST
20 N        DS      F
21          MSG     DC      C'FACTORIAL 5
22 OUT      DS      CL12

24 *
25 * DSECT TO ADDRESS GETMAIN ALLOCATIONS
26 *
27 AUTO     DSECT
28 SAVE     DS      18F              * SAVE AREA
```
```