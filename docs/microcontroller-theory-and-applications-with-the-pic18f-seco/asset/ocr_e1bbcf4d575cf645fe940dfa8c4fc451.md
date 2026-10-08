MUL    A, B, R1        ;       R1 ← A * B
MUL    C, D, R2        ;       R2 ← C * D
MUL    E, F, R3        ;       R3 ← E * F
ADD    R1, R2, R1      ;       R1 ← R1 + R2
SUB    R1, R3, Z       ;       Z ← R1 - R3

This sequence implements the statement Z = A * B + C * D - E * F. The three-address format, in addition to the other formats, is normally used by typical microcontrollers such as the PIC18F.

If we drop the third address from the three-address format, we obtain the two-address format, whose general form is
<op-code> Addr1, Addr2
Some typical two-address instructions are

MOV    A, R1           ;       R1 ← A
ADD    C, R2           ;       R2 ← R2 + C
SUB    R1, R2          ;       R2 ← R2 - R1

In this format, the addresses Addr1 and Addr2 represent source and destination addresses, respectively.

The following sequence of two-address instructions is equivalent to the program using three-address format presented earlier:

MOV    A, R1           ;       R1 ← A
MUL    B, R1           ;       R1 ← R1 * B
MOV    C, R2           ;       R2 ← C
MUL    D, R2           ;       R2 ← R2 * D
MOV    E, R3           ;       R3 ← E
MUL    F, R3           ;       R3 ← R3 * F
ADD    R2, R1          ;       R1 ← R1 + R2
SUB    R3, R1          ;       R1 ← R1 - R3
MOV    R1, Z           ;       Z ← R1

Some typical one-address instructions are

LDA    B               ;       Acc ← B
ADD    C               ;       Acc ← Acc + C
MUL    D               ;       Acc ← Acc * D
STA    E               ;       E   ← Acc

Note that Acc means the accumulator.
The following program illustrates how we can translate the C language statement, z = (a * b) + (c * d) - (e * f);, into a sequence of one-address instructions:

lda    e               ;       Acc ← e
mul    f               ;       Acc ← e * f
sta    t1              ;       t1 ← Acc
lda    c               ;       Acc ← c
mul    d               ;       Acc ← c * d
sta    t2              ;       t2 ← Acc
lda    a               ;       Acc ← a
mul    b               ;       Acc ← a * b
add    t2              ;       Acc ← Acc + t2
sub    t1              ;       Acc ← Acc - t1
sta    z               ;       Z ← Acc

In this program, t1 and t2 represent the addresses of memory locations used to store temporary results. Instructions that do not require any addresses are called zero-