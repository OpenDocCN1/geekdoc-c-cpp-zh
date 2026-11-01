
```asm
1 TITLE 'CALCULATOR'
2 PRINT NOGEN
3
4 CALC SUBENTRY
5 EQUEREGS
6
7 LOOP XREAD IN,40
8 BC B'0100',EXIT
9 XPRNT INP,L'INP+L'IN
10 LA R1,IN
11 MVI OUT,C' '
12 MVC OUT+1(L'OUT-1),OUT
13
14 XDECI R3,0(R0,R1) * FIRST OPERAND
15 BC B'001',ERR1
16 XDECO R3,OUT
17
18 XDECI R4,0(0,R1) * SECOND OPERAND
19 BC B'001',ERR2
20 XDECO R4,OUT+12
21
22 L5 CLI 0(R1),C' ' * FIND OPR
23 BNE L6
24 LA R1,1(R0,R1)
25 C R1,LIM
26 BH ERR4
27 B L5
28
29 L6 MVC OUT+27(1),0(R1)
30 MVC OUT+27(2),C'->'
31
32 CLI 0(R1),C'+'
33 BNE SUB
34
35 ADD AR R3,R4
36 XDECO R3,OUT+29
37 XPRNT OUT,L'OUT
38 B LOOP
39
40 SUB CLI 0(R1),C'-'
41 BNE MULT
42
43 SR R3,R4
44 XDECO R3,OUT+29
45 XPRNT OUT,L'OUT
46 B LOOP
47
48 MULT CLI 0(R1),C'*'
49 BNE DIV
50
51 MR R2,R4
52 XDECO R3,OUT+29
53 XPRNT OUT,L'OUT
54 B LOOP
55
56 DIV CLI 0(R1),C'/'
57 BNE MOD
58 LR R2,R3
59 SRDA R2,32
60 DR R2,R4
61 XDECO R3,OUT+29
62 XPRNT OUT,L'OUT
63 B LOOP
64
65 MOD CLI 0(R1),C'%'
66 BNE ERR3
67 LR R2,R3
68 SRDA R2,32
69 DR R2,R4
70 XDECO R2,OUT+29
71 XPRNT OUT,L'OUT
72 B LOOP
73
74 ERR1 XPRNT ERRMSG1,L'ERRMSG1
75 B EXIT
76 ERR2 XPRNT ERRMSG2,L'ERRMSG2
77 B EXIT
78 ERR3 XPRNT ERRMSG3,L'ERRMSG3
79 B EXIT
80 ERR4 XPRNT ERRMSG4,L'ERRMSG4
81
82 EXIT SUBEXIT
83 INP DC C'INPUT = '
84 IN DS CL40
85 LIM DC A(*)
86 OUT DS CL50
87
88 * ERROR MSGS
89 ERRMSG1 DC C'FIRST OPERAND INPUT ERROR'
90 ERRMSG2 DC C'SECOND OPERAND INPUT ERROR'
91 ERRMSG3 DC C'OPERATOR ERROR'
92 ERRMSG4 DC C'OPERATOR NOT FOUND'
93
94 END
```

Example output:

```
INPUT = 22 33 +
  22      33  ->      55
INPUT = 22 33 -
  22      33  ->     -11
INPUT = 22 33 *
  22      33  ->     726
INPUT = 22 33 /
  22      33  ->      0
INPUT = 22 33 %
  22      33  ->     22
```

Figure 82 Calculator Program

## 23.2 Printing Bit Strings

Figure 83 gives an example of printing bit strings for the powers of two from 0 to 20. It also illustrates calling a subroutine and passing arguments.

The main body of the program is the CSECT BIN (recall that the SUBENTRY macro includes a CSECT statement whose label is the same as that placed on the SUBENTRY itself) that extends from lines 4 through 21. We will refer to this as our main program. The subroutine is the CSECT BPRNT, contained on lines 25 through 53. The main program generates the binary powers and the subroutine converts the bits to EBCDIC zoned decimal 0s and 1s which the main program prints.

The main program BIN operates as follows:

- 1. The value of 2^0 is loaded into R6 on line 6 and R2 is zeroed on line 7.
- 2. Lines 8 through 16 are the main loop.
- 3. The decimal value of the power of two contained in R6 is written to the output field at OUT.
- 4. The address of the parameter list is loaded into R1 on line 9. The parameter list consists of one item: the address of the output field OUT. The value to be converted is passed in R6.
- 5. The address of the subroutine is loaded into R15 on line 10 and a branch is made to the subroutine on line 11 with the return address, the address of the instruction following the BASR, loaded into R14.
- 6. Upon return, the result is printed on line 12.
- 7. The value in R6 is shifted one position to the left effectively multiplying the value by two and raising it to the next power.
- 8. The counter in R2 is incremented and compared to 31. If less than, the loop repeats.

The subroutine receives a number in R6. This number is 31 zeros and one bit with a value of one. The subroutine looks at each bit of R6 from low order to high order. Based on what it finds, it sets the output string:

- 1. On entry to BPRNT, SUBENTRY saves the registers which will be restored on exit.
- 2. R1 points to the first (and only) word in the parameter list. The load on line 29 loads the value stored in the parameter list, the address of OUT, into R3 which is incremented in line 30 by 13 to point to the place after the decimal number already in OUT where we will place the printable bit string.
- 3. We place a character 0 at the location pointed to by R3 and then propagate it across the remainder of the output field (31 positions). Now the output field contains the printable decimal number followed by a blank and then 32 zeros.
- 4. We initialize R5 with 31 (line 36) and the low byte of R2 with a character one. R5 will be a counter which we will decrement. The low byte of R2 will be stored into the output string as needed.
- 5. Lines 39 through 46 are a loop which inspects each bit in R6 (passed from the main program) and, if it is one, stores a character one into the corresponding position of the 32 digit binary output string thus changing the 0 already there to 1.
- 6. The value in R6 is always 31 zeros and one bit with the value one. This value is copied to R4 and ANDed with MASK which forces the leading 31 bits to zero. Only the 32nd bit is untouched. The AND sets the condition code to reflect the result. If the result is all zeros, the last bit must have been zero. If the result is not zero, the last bit must have been a 1. If the last bit was a 1, on line 42, we store a character 1 at the position in the output pointed to by the sum of R5 and R3. R3 is the address of the portion of OUT where the bit string begins. R5 is our counter, a number that we decrement from 31. Thus, the sum of the contents of R3 and R5 are the address of the position in the output string whose bit we are examining. As R5 decrements, we will move to positions to the left. We begin at the rightmost.
- 7. On line 43 we shift the value in R6 to the right by one. This exposes the next higher order bit in R6 to our AND mask. We decrement R5 and test to see if it is zero. If greater than or equal, we branch to LOOP1 and repeat for the next bit.

```asm
1 TITLE 'PRINT BIT STRINGS'
2 PRINT NOGEN
3
4 BIN SUBENTRY
5 EQUEREGS
6 L R6,ONE * INIT R6
7 SR R2,R2 * COUNTER
8 LOOP XDECO R6,OUT * CVT R6 TO DECIMAL
9 LA R1,PARTTAB * ADDR OF PARAMETER TABLE
10 L R15,=V(BPRNT) * ADDR OF SUB
11 BASR R14,R15 * CALL SUB
12 XPRNT OUT,L'OUT * PRINT RESULT
13 SLL R6,1 * SHIFT BIT LEFT
14 A R2,=F'1' * INC COUNTER
15 C R2,=F'31' * DONE?
16 BL LOOP * NOPE
17 SUBEXIT
18 ONE DC F'1'
19 OUT DC CL45' '
20 PARTTAB DC A(OUT)
21 LTORG
22 *
23 * SUB TO PRINT BIT STRINGS
24 *
25 BPRNT SUBENTRY
26 *
27 * INITIALIZE 2ND PART OF OUT
28 *
29 L R3,0(0,R1) * ADDRESS OF OUT
30 LA R3,13(0,R3) * OUT+13
31 MVI 0(R3),C'0' * SEED CHARACTER
32 MVC 1(31,R3),0(R3) * RIPPLE MOVE
33 *
34 * INITIALIZE REGISTERS
35 *
36 LA R5,31(0,0) * COUNT
37 IC R2,CONE * LOAD CHAR 1
38 *
39 LOOP1 LR R4,R6 * COPY TO R4
40 N R4,MASK * AND WITH MASK
41 BZ L1 * LEAVE 0 IN OUT STR
42 STC R2,0(R5,R3) * PUT 1 IN OUT STR
43 L1 SRL R6,1 * SHIFT RIGHT
44 S R5,ONE1 * DEC COUNTER
45 C R5,ZERO * AT ZERO?
46 BNL LOOP1 * NOPE
47 SUBEXIT GRACIE
48 CONE DC C'1'
49 ONE1 DC F'1'
50 N32 DC F'32'
51 ZERO DC F'0'
52 DS 0F
53 MASK DC X'00000001'
54 END
```

Output

```
1 00000000000000000000000000000001
2 00000000000000000000000000000010
4 00000000000000000000000000000100
8 00000000000000000000000000001000
16 00000000000000000000000000010000
32 00000000000000000000000000100000
64 00000000000000000000000001000000
128 00000000000000000000000010000000
256 00000000000000000000000100000000
512 00000000000000000000001000000000
1024 00000000000000000000010000000000
2048 00000000000000000000100000000000
4096 00000000000000000001000000000000
8192 00000000000000000010000000000000
16384 00000000000000000100000000000000
32768 00000000000000001000000000000000
65536 00000000000000010000000000000000
131072 00000000000000100000000000000000
262144 00000000000001000000000000000000
524288 00000000000010000000000000000000
```
