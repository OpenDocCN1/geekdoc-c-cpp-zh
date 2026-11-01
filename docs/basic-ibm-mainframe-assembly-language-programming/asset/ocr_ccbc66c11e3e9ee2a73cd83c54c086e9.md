We use two labels in the macro on lines 9 and 10. Since the macro might be invoked several times in a program, these must be unique. We accomplish this with &SYNDX. The &SYNDX portion is substituted by the pre-processor with a numeric value unique to each invocation at each place where the labels AA&SYNDX or BB&SYNDX are used as seen in Figure 80. In this fragment of a listing file you can see the ENTRY macro expansion on lines 2 through 11. Note that all instances of AA&SYNDX have been replaced by AA0002 and all instances of BB&SYNDX have been replaced by BB0002.

```
1  PGM1      ENTRY
2  +PGM1      CSECT
3  +          STM     R14,R12,12(R13)
4  +          BALR    R12,R0
5  +          USING   *,R12
6  +          B       BB00002
7  +AA00002   DS      18F
8  +BB00002   LA      R14,AA00002
9  +          ST      R14,8(R13)
10 +          ST      R13,4(R14)
11 +          LR      R13,R14
..
```

Figure 80 &SYNDX Expansion

# 22.8 Example EQUREGS Macro

The purpose of the EQUREGS macro is to generate sixteen lines of the form:

```
R0 EQU 0
R1 EQU 1
R2 EQU 2
...
```

We could do this with 16 EQU statements or, as shown in Figure 81, as a macro. On line 3 we declare a local arithmetic set symbol &R and, on line 4, initialize it to zero. Lines 5 through 8 constitute a loop. Line 6 is the only line that generates code for the assembler. The lines it generates have a label constructed by the concatenation of the letter R with the numeric value of the set symbol &R followed by blanks, the string EQU and the value of &R. Thus, each time line 6 is processed by the pre-processor, another EQU statement is generated into the user's program.

The first EQU generated is for &R with a value of zero. In line 7, however, &R is incremented. On line 8 we test if the value in &R is less than 16 and, if it is, we branch to the sequence symbol